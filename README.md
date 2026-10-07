# BlazingNode Developer Guide & Code Library

> **Official Developer Hub, Architecture Reference, and Code Library for [BlazingNode](https://blazingnode.com).**  
> High-Throughput, Dedicated Bare-Metal Polygon RPC Infrastructure.

[![Polygon PoS](https://img.shields.io/badge/Polygon-Mainnet%20(137)-8247E5.svg)](https://polygon.technology/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## Documentation Reference

| Guide | Description |
| :--- | :--- |
| [**Getting Started**](docs/getting-started.md) | How to authenticate with x-api-key, format URLs, and make your first call. |
| [**Endpoints & Networks**](docs/endpoints.md) | Mainnet connection strings (HTTP and WSS) with PoP details. |
| [**Migration Guide**](docs/migration-guide.md) | Drop-in URL swap instructions in 2 minutes. |
| [**Rate Limits & Burst Handling**](docs/rate-limits-and-burst.md) | Why bare-metal nodes prevent HTTP 429 errors and reduce P95 tail latency spikes. |
| [**FAQ & Support**](docs/faq.md) | State depth, trace add-on bundles, pricing structure, and common questions. |

---

## Runnable Code Examples

Copy-paste working implementations optimized for low latency and high concurrency:

- **[Viem Client (TypeScript)](examples/viem/README.md):** Modern public client with keep-alive HTTP connections and x-api-key authentication.
- **[Ethers.js v6](examples/ethers/README.md):** Standard JsonRpcProvider with static network configuration to save roundtrips.
- **[Python Web3.py](examples/python-web3/README.md):** Trading bot client with persistent HTTP connection pooling and PoA middleware.
- **[WebSocket Subscriptions](examples/websocket/README.md):** Real-time newHeads and logs streaming with auto-reconnect logic.
- **[Concurrent JSON-RPC](examples/batch-rpc/README.md):** How to dispatch parallel calls taking advantage of 300 RPS burst headroom.

---

## Security & Privacy

BlazingNode does not log private transaction payloads or frontrun user transactions. Dedicated bare-metal instances offer isolated compute and memory with no noisy neighbors.

For technical support & inquiries: `support@blazingnode.com` (or `daniel@blazingnode.com`)

---

## License
MIT © [BlazingNode](https://blazingnode.com)
