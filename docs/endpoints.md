# Network Endpoints & Chain Specifications

BlazingNode operates dedicated bare-metal nodes connected directly to high-capacity tier-1 transit backbones.

---

## Network Overview

| Parameter | Polygon PoS Mainnet | Polygon Amoy Testnet |
| :--- | :--- | :--- |
| **Chain ID** | `137` (`0x89`) | `80002` (`0x13882`) |
| **Native Currency** | POL (formerly MATIC) | POL (Testnet) |
| **Block Time** | ~2.0 seconds | ~2.0 seconds |
| **Consensus Clients** | Heimdall v2 + Bor | Heimdall v2 + Bor |

---

## Connection Endpoints
 
### 1. Polygon Mainnet (Chain ID 137)

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

### 2. Polygon Amoy Testnet (Chain ID 80002)

#### HTTPS Endpoint
```text
https://polygon-amoy.blazingnode.com/{API_KEY}
```

#### WebSocket (WSS) Endpoint
```text
wss://polygon-amoy.blazingnode.com/ws/{API_KEY}
```

---

## Geographic PoPs & Routing

BlazingNode nodes are deployed on dedicated bare-metal servers strategically positioned near major crypto liquidity hubs:

- **North America East:** Beauharnois / Montreal (BHS) & Ashburn (IAD)
- **Europe:** Frankfurt (FRA) & London (LDN)

All inbound DNS requests use geo-anycast latency routing to automatically connect your server or bot to the closest physical bare-metal instance.
