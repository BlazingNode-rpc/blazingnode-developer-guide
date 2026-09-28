# Getting Started with BlazingNode

Welcome to the **BlazingNode Developer Guide**. BlazingNode delivers enterprise-grade, bare-metal dedicated Polygon RPC infrastructure designed for low-latency trading bots, high-throughput MEV systems, data indexers, and production dApps.

---

## 1. Authentication & API Key Model

Every request to BlazingNode requires your dedicated authentication key. BlazingNode supports both URL-embedded keys and HTTP header-based authentication.

### Option A: URL Path Authentication (Recommended for standard libraries)
```text
https://polygon.blazingnode.com/YOUR_API_KEY
```

### Option B: WebSocket Path Authentication
```text
wss://polygon.blazingnode.com/ws/YOUR_API_KEY
```

### Option C: Header Authentication (Recommended for custom proxies)
```http
POST / HTTP/1.1
Host: polygon.blazingnode.com
Content-Type: application/json
x-api-key: YOUR_API_KEY

{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}
```

---

## 2. Quick Verification (cURL)

Test your connection from your local terminal or VPS server:

```bash
curl -X POST https://polygon.blazingnode.com/YOUR_API_KEY \
  -H "Content-Type: application/json" \
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

- [**Viem (TypeScript)**](../examples/viem/README.md) - Modern, type-safe EVM client with automatic batching and fallback support.
- [**Ethers.js v6 (JavaScript/TypeScript)**](../examples/ethers/README.md) - Standard JsonRpcProvider with retry logic.
- [**Python Web3.py**](../examples/python-web3/README.md) - Asynchronous or synchronous Web3 connection for trading bots.
- [**WebSocket Subscriptions**](../examples/websocket/README.md) - Persistent low-latency block head (`newHeads`) and log filters.
- [**High-Throughput Batching**](../examples/batch-rpc/README.md) - Parallel JSON-RPC multichunk queries without socket stalls.

---

## 4. Benchmark Your Connection

Before deploying bots to production, verify your roundtrip latency and P95 distribution using our open-source benchmark CLI:

```bash
npx blazing-bench --target "https://polygon.blazingnode.com/YOUR_API_KEY"
```

> 🎁 **Developer Incentive:** Share your benchmark report with `engineering@blazingnode.com` to claim a **Free 72-Hour Burst Pass (+100 RPS)** or **20M Volume Pack**. Learn more at [blazingnode.com/benchmark-submit](https://blazingnode.com/benchmark-submit).
