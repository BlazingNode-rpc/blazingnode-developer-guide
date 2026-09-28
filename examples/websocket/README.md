# WebSocket Listener with Auto-Reconnect

Low-latency real-time event streaming (`newHeads` and `logs`) over persistent WebSockets.

---

## 1. Installation

```bash
npm install ws
```

---

## 2. Configuration (`ws_listener.js`)

```javascript
import WebSocket from 'ws';

const WSS_URL = process.env.BLAZINGNODE_WSS || 'wss://polygon.blazingnode.com/ws/YOUR_API_KEY';

function connect() {
  console.log(`📡 Connecting to BlazingNode WSS: ${WSS_URL}...`);
  const ws = new WebSocket(WSS_URL);

  ws.on('open', () => {
    console.log('✅ WebSocket Connected. Subscribing to newHeads...');
    
    // Subscribe to new block headers
    ws.send(JSON.stringify({
      jsonrpc: '2.0',
      id: 1,
      method: 'eth_subscribe',
      params: ['newHeads']
    }));
  });

  ws.on('message', (data) => {
    const msg = JSON.parse(data.toString());
    if (msg.params && msg.params.result) {
      const header = msg.params.result;
      const blockNum = parseInt(header.number, 16);
      console.log(`📦 New Block: #${blockNum} | Hash: ${header.hash} | Gas: ${parseInt(header.gasUsed, 16)}`);
    } else {
      console.log('Ack:', msg);
    }
  });

  ws.on('close', () => {
    console.log('⚠️ WebSocket closed. Reconnecting in 2 seconds...');
    setTimeout(connect, 2000);
  });

  ws.on('error', (err) => {
    console.error('Socket error:', err.message);
    ws.terminate();
  });
}

connect();
```
