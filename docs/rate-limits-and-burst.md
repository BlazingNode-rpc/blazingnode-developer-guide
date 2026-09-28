# Rate Limits, Burst Handling & Concurrency

Most RPC providers advertise enormous monthly limits (e.g. 100M compute units) but implement tight, undisclosed **per-second concurrency caps**.

When market volatility strikes or an arbitrage window opens, bots firing 50+ requests per second suddenly receive `HTTP 429 Too Many Requests`, causing missed trades or stuck transactions.

---

## The BlazingNode Bare-Metal Difference

BlazingNode does not run on overloaded multi-tenant virtual machines. Our nodes are deployed on dedicated physical servers equipped with:
- Dedicated enterprise NVMe storage arrays (>1,000,000 IOPS).
- High single-thread clock speeds (ideal for Bor's EVM execution engine).
- Dedicated gigabit network pipelines directly peered with Tier-1 IP transit.

### Comparison Table

| Metric | Typical Shared Tier | BlazingNode High-Throughput |
| :--- | :--- | :--- |
| **Max Concurrent Sockets** | 5 – 10 sockets | 100+ concurrent connections |
| **Burst Ceiling** | 25 – 40 RPS | 100 – 250+ RPS sustained |
| **HTTP 429 Throttle Strategy** | Instant hard cutoff | Generous burst buffers |
| **Socket Drop / Reset** | Frequent on high volume | Zero artificial connection resets |

---

## Best Practices for High-Throughput Bots

1. **Enable HTTP Keep-Alive:**
   Re-using TLS connections reduces latency by 20–50ms per call. Always pass a persistent `http.Agent` in Node.js or `requests.Session` in Python.
2. **Utilize JSON-RPC Batching:**
   Combine 10–50 calls (`eth_getBalance`, `eth_call`) into a single HTTP POST request to minimize TCP roundtrip overhead. See [High-Throughput Batching Example](../examples/batch-rpc/README.md).
3. **Use WebSockets for Event Monitoring:**
   Instead of polling `eth_blockNumber` every 500ms, subscribe to `eth_subscribe("newHeads")` over WSS.
