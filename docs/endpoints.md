# Network Endpoints & Chain Specifications

BlazingNode operates dedicated bare-metal nodes connected directly to high-capacity tier-1 transit backbones.

---

## Network Overview

| Parameter | Polygon PoS Mainnet |
| :--- | :--- |
| **Chain ID** | `137` (`0x89`) |
| **Native Currency** | POL (formerly MATIC) |
| **Block Time** | ~2.0 seconds |
| **Consensus Clients** | Heimdall v2 + Bor |

---

## Connection Endpoints
 
### Polygon Mainnet (Chain ID 137)

#### HTTPS Endpoint
```text
https://rpc.blazingnode.com
```
- **Header:** `x-api-key: YOUR_API_KEY`
- **Protocols:** HTTP/1.1, HTTP/2, HTTP/3 (QUIC)
- **Supported Methods:** Full Ethereum JSON-RPC spec (`eth_*`, `net_*`, `web3_*`, Bor-specific tracing).

#### WebSocket (WSS) Endpoint
```text
wss://rpc.blazingnode.com/ws
```
- **Handshake Header:** `x-api-key: YOUR_API_KEY` (or query param `?key=YOUR_API_KEY`)
- **Heartbeat:** Built-in ping/pong frames every 30 seconds.
- **Subscriptions Supported:** `eth_subscribe` (`newHeads`, `logs`, `newPendingTransactions`).

---

## Infrastructure & Deployment

BlazingNode nodes are deployed on dedicated bare-metal servers in our high-capacity Northeast cluster.
