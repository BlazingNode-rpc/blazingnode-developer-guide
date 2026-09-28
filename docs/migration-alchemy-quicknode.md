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

## 3. Why High-Throughput Bots Migrate to BlazingNode

| Feature | Virtualized / Shared RPCs (Alchemy, QuickNode) | BlazingNode Dedicated Bare-Metal |
| :--- | :--- | :--- |
| **Infrastructure** | Multi-tenant cloud hypervisors (AWS/GCP) | Dedicated physical hardware (NVMe + high-clock CPUs) |
| **Burst Capacity** | Frequent HTTP 429 throttling on sudden traffic spikes | Sustained 100+ RPS without drops |
| **P95 / P99 Tail Latency** | High variance due to "noisy neighbors" on shared VM pools | Flat, predictable sub-30ms latency |
| **Stale Block Head** | Cached responses occasionally lag behind tip | True live head direct from Bor/Heimdall |
| **Pricing Predictability** | Variable compute units (CUs) that explode during volatility | Predictable flat-rate dedicated packages |
