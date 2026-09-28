## 1. Switching HTTP Endpoints

### Endpoint Pattern
- **Previous Provider:** `https://your-provider.com/v2/YOUR_KEY`
- **BlazingNode:** `https://rpc.blazingnode.com` (pass `x-api-key: YOUR_KEY` in header)

### Viem Example
```typescript
import { createPublicClient, http } from 'viem';
import { polygon } from 'viem/chains';

export const client = createPublicClient({
  chain: polygon,
  transport: http('https://rpc.blazingnode.com', {
    fetchOptions: {
      headers: {
        'x-api-key': process.env.BLAZINGNODE_API_KEY!,
      },
    },
  }),
});
```

### Ethers.js v6 Example
```javascript
import { ethers } from 'ethers';

const network = ethers.Network.from(137);
const fetchReq = new ethers.FetchRequest('https://rpc.blazingnode.com');
fetchReq.setHeader('x-api-key', process.env.BLAZINGNODE_API_KEY);

export const provider = new ethers.JsonRpcProvider(fetchReq, network, {
  staticNetwork: network,
});
```

---

## 2. Switching WebSocket (WSS) Endpoints

- **Previous WSS:** `wss://your-provider.com/ws/YOUR_KEY`
- **BlazingNode WSS:** `wss://rpc.blazingnode.com/ws` (pass `x-api-key: YOUR_KEY` or `?key=YOUR_KEY`)

```javascript
import WebSocket from 'ws';

const ws = new WebSocket('wss://rpc.blazingnode.com/ws', {
  headers: {
    'x-api-key': process.env.BLAZINGNODE_API_KEY,
  },
});
```

---

## 3. Architecture Benefits for High-Throughput Bots

- **Dedicated Physical Hardware:** Enterprise NVMe drives and dedicated CPU cores ensure zero contention from noisy neighbors.
- **Sustained Concurrency:** Run 100+ concurrent connections without arbitrary socket resets.
- **Predictable Tail Latency:** Sub-30ms P50 latency with flat, predictable P95 distributions under peak market volume.
- **Clean Head Tracking:** Direct Bor client reads with zero stale-block caching.
