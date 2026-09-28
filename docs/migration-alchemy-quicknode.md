# Migrating from Alchemy, QuickNode, or Infura in 2 Minutes

Switching to BlazingNode is a **drop-in URL swap**. Because BlazingNode strictly adheres to standard Ethereum & Polygon JSON-RPC specifications, **no code rewrites or SDK changes are required**.

---

## 1. Alchemy Migration

### URL Pattern Comparison
- **Alchemy:** `https://polygon-mainnet.g.alchemy.com/v2/YOUR_ALCHEMY_KEY`
- **BlazingNode:** `https://polygon.blazingnode.com/YOUR_BLAZING_KEY`

### Viem Example
```diff
- const rpcUrl = "https://polygon-mainnet.g.alchemy.com/v2/" + process.env.ALCHEMY_API_KEY;
+ const rpcUrl = "https://polygon.blazingnode.com/" + process.env.BLAZINGNODE_API_KEY;

  export const client = createPublicClient({
    chain: polygon,
    transport: http(rpcUrl),
  });
```

### Ethers.js v6 Example
```diff
- const provider = new ethers.JsonRpcProvider("https://polygon-mainnet.g.alchemy.com/v2/" + process.env.ALCHEMY_API_KEY);
+ const provider = new ethers.JsonRpcProvider("https://polygon.blazingnode.com/" + process.env.BLAZINGNODE_API_KEY);
```

---

## 2. QuickNode Migration

### URL Pattern Comparison
- **QuickNode:** `https://your-endpoint.matic.quiknode.pro/YOUR_TOKEN/`
- **BlazingNode:** `https://polygon.blazingnode.com/YOUR_BLAZING_KEY`

### WebSocket Migration
- **QuickNode WSS:** `wss://your-endpoint.matic.quiknode.pro/YOUR_TOKEN/`
- **BlazingNode WSS:** `wss://polygon.blazingnode.com/ws/YOUR_BLAZING_KEY`

```diff
- const wsUrl = "wss://your-endpoint.matic.quiknode.pro/" + process.env.QUICKNODE_TOKEN;
+ const wsUrl = "wss://polygon.blazingnode.com/ws/" + process.env.BLAZINGNODE_API_KEY;
```

---

## 3. Why High-Throughput Bots Migrate to BlazingNode

| Feature | Virtualized / Shared RPCs (Alchemy, QuickNode) | BlazingNode Dedicated Bare-Metal |
| :--- | :--- | :--- |
| **Infrastructure** | Multi-tenant cloud hypervisors (AWS/GCP) | Dedicated physical hardware (NVMe + high-clock CPUs) |
| **Burst Capacity** | Frequent HTTP 429 throttling on sudden traffic spikes | Sustained 100+ RPS without drops |
| **P95 / P99 Tail Latency** | High variance due to "noisy neighbors" on shared VM pools | Flat, predictable sub-30ms latency |
| **Stale Block Head** | Cached responses occasionally lag behind tip | True live head direct from Bor/Heimdall |
| **Pricing Predictability** | Variable compute units (CUs) that explode during volatility | Predictable flat-rate dedicated packages |
