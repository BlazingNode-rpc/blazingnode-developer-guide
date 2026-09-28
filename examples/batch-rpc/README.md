# High-Throughput Batch JSON-RPC

Learn how to batch multiple JSON-RPC calls into a single HTTP roundtrip to avoid TCP overhead and socket exhaustion.

---

## Direct cURL Multi-Call Batch

```bash
curl -X POST https://polygon.blazingnode.com/YOUR_API_KEY \
  -H "Content-Type: application/json" \
  -d '[
    {"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1},
    {"jsonrpc":"2.0","method":"eth_gasPrice","params":[],"id":2},
    {"jsonrpc":"2.0","method":"eth_chainId","params":[],"id":3}
  ]'
```

---

## Node.js Batch Script (`batch.js`)

```javascript
const RPC_URL = process.env.BLAZINGNODE_RPC || 'https://polygon.blazingnode.com/YOUR_API_KEY';

async function executeBatch() {
  const batchRequests = [
    { jsonrpc: '2.0', id: 1, method: 'eth_blockNumber', params: [] },
    { jsonrpc: '2.0', id: 2, method: 'eth_gasPrice', params: [] },
    { jsonrpc: '2.0', id: 3, method: 'eth_chainId', params: [] },
  ];

  console.log(`⚡ Sending ${batchRequests.length} requests in 1 roundtrip...`);
  const start = performance.now();

  const response = await fetch(RPC_URL, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(batchRequests),
  });

  const results = await response.json();
  const elapsed = (performance.now() - start).toFixed(1);

  console.log(`✅ Batch complete in ${elapsed}ms:`);
  console.log(results);
}

executeBatch().catch(console.error);
```
