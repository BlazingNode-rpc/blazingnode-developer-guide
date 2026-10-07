# Frequently Asked Questions (FAQ) & Support

### Q: Why do I receive HTTP 429 errors from my existing provider?
**A:** Most shared providers implement aggressive Token Bucket rate limiters to protect multi-tenant infrastructure from being overloaded by a single user. Even if you have millions of unused monthly requests, bursting above 25–40 RPS triggers immediate HTTP 429 rejections. BlazingNode dedicates physical bare-metal hardware, allowing 300 RPS burst headroom on all plans without artificial throttling.

### Q: What is the difference between average latency and P95 tail latency?
**A:** Average latency (mean) looks deceptively low because simple, cached queries bring down the math. However, during high-volatility events, trading bots fire concurrent bundles of state reads. **P95 latency** measures the slowest 5% of your requests—which is when your bot is most vulnerable to timeouts. BlazingNode maintains flat, predictable P95 latencies even under 20+ parallel requests.

### Q: Does BlazingNode support Archive data?
**A:** Yes, BlazingNode provides full historical state access for Polygon PoS. You can execute `eth_call` and `eth_getLogs` at any historical block height without missing-trie errors.

### Q: Do you support debug_traceTransaction or trace_block?
**A:** Yes, high-performance tracing methods are supported on dedicated instances for MEV searchers and analytical indexers. Contact `daniel@blazingnode.com` for custom tracing requirements.

### Q: What is the recommended fallback strategy?
**A:** In mission-critical trading, never rely on a single provider. We recommend placing BlazingNode as your primary high-speed tier, with an automatic fallback client configured to route traffic to a secondary provider if network anomalies occur. See our [Viem Fallback Example](../examples/viem/README.md).

---

## Technical Support

- **Email:** `daniel@blazingnode.com`
- **Website:** [blazingnode.com](https://blazingnode.com)
- **GitHub Issues:** [BlazingNode-rpc/blazingnode-developer-guide/issues](https://github.com/BlazingNode-rpc/blazingnode-developer-guide/issues)
