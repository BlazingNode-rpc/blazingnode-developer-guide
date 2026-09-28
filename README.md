# BlazingNode Developer Guide & Code Library

> **Official Developer Hub, Architecture Reference, and Code Library for [BlazingNode](https://blazingnode.com).**  
> High-Throughput, Dedicated Bare-Metal Polygon RPC Infrastructure.

[![Polygon PoS](https://img.shields.io/badge/Polygon-Mainnet%20(137)-8247E5.svg)](https://polygon.technology/)
[![Polygon Amoy](https://img.shields.io/badge/Polygon-Amoy%20(80002)-blue.svg)](https://amoy.polygonscan.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Benchmark Tool](https://img.shields.io/badge/Benchmark-blazingnode--bench-orange.svg)](https://github.com/BlazingNode-rpc/benchmark-cli)

---

## Benchmark Switcher Offer

> **Switch to BlazingNode with Your Benchmark Report:**  
> Run the benchmark against your current endpoint, start your evaluation, and send your report to **`daniel@blazingnode.com`**:
> - **Bonus Capacity:** When you subscribe to any paid plan (Builder, Operator, or Pro), Daniel will credit a **bonus 20M Volume Pack** directly to your account.
> - **Run Benchmark:** `npx blazingnode-bench --target <YOUR_CURRENT_RPC>`
> - **Sign Up:** [https://blazingnode.com/signup](https://blazingnode.com/signup)

---

## Documentation Reference

| Guide | Description |
| :--- | :--- |
| [**Getting Started**](docs/getting-started.md) | How to authenticate, format URLs, pass API keys, and make your first call. |
| [**Endpoints & Networks**](docs/endpoints.md) | Mainnet & Amoy testnet connection strings (HTTP and WSS) with PoP details. |
| [**Migration Guide**](docs/migration-alchemy-quicknode.md) | Drop-in URL swap instructions in 2 minutes. |
| [**Rate Limits & Burst Handling**](docs/rate-limits-and-burst.md) | Why bare-metal nodes prevent HTTP 429 errors and reduce P95 tail latency spikes. |
| [**FAQ & Support**](docs/faq.md) | Archive access, debug_trace support, fallback strategy, and support contacts. |

---

## Runnable Code Examples

Copy-paste working implementations optimized for low latency and high concurrency:

- **[Viem Client (TypeScript)](examples/viem/README.md):** Modern public client with automatic batching and fallback provider support.
- **[Ethers.js v6](examples/ethers/README.md):** Standard JsonRpcProvider with static network configuration to save roundtrips.
- **[Python Web3.py](examples/python-web3/README.md):** Trading bot client with persistent HTTP connection pooling.
- **[WebSocket Subscriptions](examples/websocket/README.md):** Real-time newHeads and logs streaming with auto-reconnect logic.
- **[Batch JSON-RPC](examples/batch-rpc/README.md):** How to bundle 10–50 calls into single HTTP roundtrips.

---

## Benchmark Your Current Node

Compare your existing RPC provider directly against BlazingNode across three crucial vectors:

```bash
# Run instantly with zero install
npx blazingnode-bench --target "https://your-provider-rpc-url.com/YOUR_KEY"
```

1. **P95 Tail Latency:** Concurrency pools of 10 and 20 parallel calls.
2. **Block Head Freshness:** Detects stale block reads against the canonical Polygon head.
3. **Burst Stress Test:** Ramps from 25 RPS to 100+ RPS to reveal artificial HTTP 429 throttling.

Full benchmark source code: [BlazingNode-rpc/benchmark-cli](https://github.com/BlazingNode-rpc/benchmark-cli).

---

## Security & Privacy

BlazingNode does not log private transaction payloads or frontrun user transactions. Dedicated bare-metal instances offer isolated compute and memory with no noisy neighbors.

For security reports: `security@blazingnode.com`  
For technical support & onboarding: `daniel@blazingnode.com`

---

## License
MIT © [BlazingNode](https://blazingnode.com)
