# Ethers.js v6 Integration

Standard Ethers.js v6 implementation for connecting to BlazingNode Polygon RPC.

---

## 1. Installation

```bash
npm install ethers dotenv
```

---

## 2. Configuration (`provider.js`)

```javascript
import { ethers } from 'ethers';

const RPC_URL = process.env.BLAZINGNODE_RPC || 'https://polygon.blazingnode.com/YOUR_API_KEY';

// Initialize provider with static network definition to skip extra getNetwork roundtrips
const network = ethers.Network.from(137); // Polygon Mainnet
const provider = new ethers.JsonRpcProvider(RPC_URL, network, {
  staticNetwork: network,
  batchMaxCount: 50,
});

async function run() {
  console.log(`Connecting to BlazingNode: ${RPC_URL}...`);
  const start = performance.now();

  const blockNumber = await provider.getBlockNumber();
  const feeData = await provider.getFeeData();

  const elapsed = (performance.now() - start).toFixed(1);
  console.log(`✅ Tip Block: #${blockNumber}`);
  console.log(`⛽ Max Priority Fee: ${ethers.formatUnits(feeData.maxPriorityFeePerGas ?? 0n, 'gwei')} Gwei`);
  console.log(`⏱️ Latency: ${elapsed}ms`);
}

run().catch(console.error);
```
