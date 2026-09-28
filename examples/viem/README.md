# Viem Client Integration (TypeScript)

This example demonstrates how to configure a high-performance Viem public client with automatic JSON-RPC batching and fallback provider support.

---

## 1. Installation

```bash
npm install viem dotenv
npm install -D typescript @types/node tsx
```

---

## 2. Configuration (`client.ts`)

```typescript
import { createPublicClient, http, fallback } from 'viem';
import { polygon } from 'viem/chains';

const BLAZINGNODE_KEY = process.env.BLAZINGNODE_API_KEY || 'YOUR_API_KEY';
const BACKUP_RPC = process.env.BACKUP_RPC || 'https://polygon-bor-rpc.publicnode.com';

// Configure high-performance client with batching and failover
export const client = createPublicClient({
  chain: polygon,
  transport: fallback([
    // Primary Tier: BlazingNode bare-metal with keep-alive batching & x-api-key
    http('https://rpc.blazingnode.com', {
      fetchOptions: {
        headers: {
          'x-api-key': BLAZINGNODE_KEY,
        },
      },
      batch: {
        batchSize: 50,
        wait: 10, // Wait 10ms to aggregate calls into single HTTP roundtrip
      },
      retryCount: 2,
      retryDelay: 150,
    }),
    // Secondary Tier: Public fallback
    http(BACKUP_RPC, {
      retryCount: 1,
    }),
  ]),
});

async function main() {
  console.log('⚡ Querying Polygon Mainnet via BlazingNode...');
  const start = performance.now();

  const [blockNumber, gasPrice] = await Promise.all([
    client.getBlockNumber(),
    client.getGasPrice(),
  ]);

  const elapsed = (performance.now() - start).toFixed(1);
  console.log(`✅ Current Block: #${blockNumber}`);
  console.log(`⛽ Gas Price: ${Number(gasPrice) / 1e9} Gwei`);
  console.log(`⏱️ Roundtrip Latency: ${elapsed}ms`);
}

main().catch(console.error);
```

---

## 3. Run the Example

```bash
BLAZINGNODE_RPC="https://polygon.blazingnode.com/YOUR_KEY" npx tsx client.ts
```
