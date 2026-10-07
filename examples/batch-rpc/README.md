# High-Throughput Concurrent JSON-RPC

Learn how to dispatch concurrent parallel JSON-RPC calls over keep-alive HTTP pipelines to leverage BlazingNode's 300 RPS burst headroom without socket stalls.

---

## Direct cURL Multi-Call (Parallel)

```bash
# Execute simultaneous requests in parallel
curl -s -X POST https://rpc.blazingnode.com \
  -H "Content-Type: application/json" \
  -H "x-api-key: YOUR_API_KEY" \
  -d '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}' &

curl -s -X POST https://rpc.blazingnode.com \
  -H "Content-Type: application/json" \
  -H "x-api-key: YOUR_API_KEY" \
  -d '{"jsonrpc":"2.0","method":"eth_gasPrice","params":[],"id":2}' &

wait
```

---

## Node.js High-Throughput Script (`concurrent.js`)

```javascript
const RPC_URL = 'https://rpc.blazingnode.com';
const API_KEY = process.env.BLAZINGNODE_API_KEY || 'YOUR_API_KEY';

async function executeConcurrent() {
  const requests = [
    { id: 1, method: 'eth_blockNumber', params: [] },
    { id: 2, method: 'eth_gasPrice', params: [] },
    { id: 3, method: 'eth_chainId', params: [] },
  ];

  console.log(`⚡ Dispatching ${requests.length} parallel requests...`);
  const start = performance.now();

  const results = await Promise.all(
    requests.map(async (req) => {
      const response = await fetch(RPC_URL, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'x-api-key': API_KEY,
        },
        body: JSON.stringify({
          jsonrpc: '2.0',
          id: req.id,
          method: req.method,
          params: req.params,
        }),
      });
      return response.json();
    })
  );

  const elapsed = (performance.now() - start).toFixed(1);
  console.log(`✅ All ${requests.length} requests resolved concurrently in ${elapsed}ms:`);
  console.log(results);
}

executeConcurrent().catch(console.error);
```
