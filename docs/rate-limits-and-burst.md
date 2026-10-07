# Rate Limits, Burst Handling & Concurrency

Most RPC providers advertise enormous monthly limits (e.g. 100M compute units) but implement tight, undisclosed **per-second concurrency caps**.

When market volatility strikes or an arbitrage window opens, bots firing 50+ requests per second suddenly receive `HTTP 429 Too Many Requests`, causing missed trades or stuck transactions.

---

## The BlazingNode Bare-Metal Difference

BlazingNode does not run on overloaded multi-tenant virtual machines. Our nodes are deployed on dedicated physical servers equipped with:
- Dedicated enterprise NVMe storage arrays (>1,000,000 IOPS).
- High single-thread clock speeds (ideal for Bor's EVM execution engine).
- Dedicated gigabit network pipelines directly peered with Tier-1 IP transit.

### Concurrency & Capacity Overview

| Parameter | Standard Shared Tiers | BlazingNode Dedicated Bare-Metal |
| :--- | :--- | :--- |
| **Concurrent Connections** | 5 – 10 sockets | High concurrent socket allocations per plan |
| **Burst Headroom** | 25 – 40 RPS | 300 RPS burst headroom on all plans |
| **Rate Limit Behavior** | Artificial 429 throttling on spikes | Sustained throughput without artificial drops |
| **Hardware Isolation** | Multi-tenant shared virtual machines | Dedicated bare-metal physical NVMe hardware |

---

## Best Practices for High-Throughput Bots

1. **Enable HTTP Keep-Alive:**
   Re-using TLS connections reduces latency by 20–50ms per call. Always pass a persistent `http.Agent` in Node.js or `requests.Session` in Python.
2. **Leverage Concurrent Parallel Pipelines:**
   Dispatch parallel async calls (`eth_getBalance`, `eth_call`) concurrently over persistent HTTP keep-alive connections to take full advantage of BlazingNode's 300 RPS burst headroom. See [High-Throughput Concurrent Example](../examples/batch-rpc/README.md).
3. **Use WebSockets for Event Monitoring:**
   Instead of polling `eth_blockNumber` every 500ms, subscribe to `eth_subscribe("newHeads")` over WSS.
