# Getting Started with BlazingNode

Welcome to the **BlazingNode Developer Guide**. BlazingNode delivers enterprise-grade, bare-metal dedicated Polygon RPC infrastructure designed for low-latency trading bots, high-throughput MEV systems, data indexers, and production dApps.

---

## 1. Authentication & API Key Model

Every request to BlazingNode requires your dedicated authentication key passed via standard HTTP header.

### HTTPS Authentication
- **Endpoint:** `https://rpc.blazingnode.com`
- **Header:** `x-api-key: YOUR_API_KEY`

```http
POST / HTTP/1.1
Host: rpc.blazingnode.com
Content-Type: application/json
x-api-key: YOUR_API_KEY

{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}
```

### WebSocket (WSS) Authentication
- **Endpoint:** `wss://rpc.blazingnode.com/ws`
- **Handshake Header:** `x-api-key: YOUR_API_KEY` (or query param `?key=YOUR_API_KEY`)

---

## 2. Quick Verification (cURL)

Test your connection from your local terminal or VPS server:

```bash
curl -X POST https://rpc.blazingnode.com \
  -H "Content-Type: application/json" \
  -H "x-api-key: YOUR_API_KEY" \
  -d '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'
```

**Expected Response:**
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x5a371ec"
}
```

---

## 3. Recommended Client Library Quickstarts

Jump straight to runnable code in our [`examples/`](../examples/) directory:

- [**Viem (TypeScript)**](../examples/viem/README.md) - Modern, type-safe EVM client with keep-alive HTTP connections and fallback support.
- [**Ethers.js v6 (JavaScript/TypeScript)**](../examples/ethers/README.md) - Standard JsonRpcProvider with retry logic.
- [**Python Web3.py**](../examples/python-web3/README.md) - Optimized Web3 connection with PoA middleware for trading bots.
- [**WebSocket Subscriptions**](../examples/websocket/README.md) - Persistent low-latency block head (`newHeads`) and log filters.
- [**High-Throughput Concurrent RPC**](../examples/batch-rpc/README.md) - Parallel JSON-RPC queries leveraging 300 RPS burst headroom without socket stalls.

---

## 4. Benchmark Your Connection

Before deploying bots to production, verify your roundtrip latency and P95 distribution using our open-source benchmark CLI:

```bash
npx blazingnode-bench --target "https://your-current-rpc-provider.com/YOUR_KEY"
```
