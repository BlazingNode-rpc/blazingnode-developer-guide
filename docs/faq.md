# Frequently Asked Questions (FAQ) & Architecture Details

### Q: Why do I receive HTTP 429 errors from my existing provider?
**A:** Most shared providers implement aggressive Token Bucket rate limiters to protect multi-tenant infrastructure from being overloaded by a single user. Even if you have millions of unused monthly requests, bursting above 25–40 RPS triggers immediate HTTP 429 rejections. BlazingNode dedicates physical bare-metal hardware, allowing 300 RPS burst headroom on all plans without artificial throttling.

### Q: What is the difference between average latency and P95 tail latency?
**A:** Average latency (mean) looks deceptively low because simple, cached queries bring down the math. However, during high-volatility events, trading bots fire concurrent bundles of state reads. **P95 latency** measures the slowest 5% of your requests—which is when your bot is most vulnerable to timeouts. BlazingNode maintains flat, predictable P95 latencies even under 20+ parallel requests.

### Q: Does BlazingNode carry full historical archive state? How many blocks are kept live?
**A:** No, BlazingNode is engineered as an ultra-fast, high-throughput execution node for live trading, bots, indexing, and recent data verification—it is not an archive node. 
- **Live Block & Execution History:** We keep **100,000 blocks (~2.25 days)** of live blocks, transactions, logs, and state available for immediate execution and block traces (`debug_traceBlockByNumber`, `trace_block`, etc.) with zero missing-trie errors.
- **Historical Block & Receipt Data (`eth_getBlockByNumber`, `eth_getTransactionReceipt`):** Accessible across full recent weeks and months on high-speed disk.
- **Deep Historical Trie State (>2.25 days):** If your workload requires running `eth_call` or storage inspections against historical contract state from weeks or months in the past, an archive node is required.

### Q: How do Trace and Debug methods work? Do they burn through my monthly budget?
**A:** You can purchase **Trace Call Bundles** that **never expire**—they simply deplete with actual usage. This ensures a 100% predictable cost structure with no surprise overages or hidden multipliers. 
- Core plans include monthly trace allowances (e.g., 25K on Builder, 50K on Operator, 100K on Pro, 250K on Business).
- When you need extra trace volume for backfills or MEV inspection, you recharge prepaid bundles (from 50K traces up to 3M traces) that stay active in your balance until used. See [Trace Add-Ons](https://blazingnode.com/pricing/trace-add-ons).

### Q: How quickly can I get to a first request?
**A:** Usually under 2 minutes once your key is created. The flow is: create account, create key, send a standard JSON-RPC request with your `x-api-key` header.

### Q: Do I need to learn a custom API?
**A:** No. BlazingNode uses standard Ethereum-style JSON-RPC for Polygon PoS. All standard methods (`eth_blockNumber`, `eth_call`, `eth_getBalance`, `eth_sendRawTransaction`, etc.) and Bor-specific extensions use the exact same payloads and formats you already use.

### Q: Where does the API key go?
**A:** Send it in the `x-api-key` HTTP header on every POST request:
```bash
curl -X POST https://rpc.blazingnode.com \
  -H "Content-Type: application/json" \
  -H "x-api-key: YOUR_API_KEY" \
  -d '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'
```
For WebSockets, pass `x-api-key` in connection headers or append `?key=YOUR_API_KEY` to the URL. If the key is missing or invalid, the request returns HTTP 401 `{"error":{"code":-32001,"message":"invalid_api_key"}}`.

### Q: Do I need to reason about compute units (CUs) or credit multipliers?
**A:** No. BlazingNode bills on clean, direct request counts (1 call = 1 request). You do not have to calculate complex credit weights, compute units, or dynamic method multipliers.

### Q: Does each plan include a dedicated Polygon node?
**A:** Current public plans run on BlazingNode’s high-throughput bare-metal Polygon cluster with authenticated access, isolated compute headroom, and plan-specific RPS and monthly request allowances. Fully dedicated private bare-metal instances can be provisioned upon request.

### Q: What if my client reports a certificate validation problem?
**A:** BlazingNode endpoints use globally trusted TLS certificates issued through our CDN edge pipeline. Always verify your system's CA certificates rather than disabling TLS verification in production.

---

## Technical Support

- **Email:** `support@blazingnode.com` (or `daniel@blazingnode.com`)
- **Website:** [blazingnode.com](https://blazingnode.com)
- **GitHub Issues:** [BlazingNode-rpc/blazingnode-developer-guide/issues](https://github.com/BlazingNode-rpc/blazingnode-developer-guide/issues)
