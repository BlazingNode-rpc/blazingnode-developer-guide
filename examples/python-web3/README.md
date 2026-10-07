# Python Web3.py Integration

Optimized connection for algorithmic trading and arbitrage bots written in Python.

---

## 1. Installation

```bash
pip install web3 requests
```

---

## 2. Configuration (`bot_provider.py`)

```python
import os
import time
from web3 import Web3
from requests import Session
from requests.adapters import HTTPAdapter

from web3.middleware import ExtraDataToPOAMiddleware

RPC_URL = "https://rpc.blazingnode.com"
API_KEY = os.getenv("BLAZINGNODE_API_KEY", "YOUR_API_KEY")

# Create a pooled session to keep TCP connections hot with x-api-key header
session = Session()
session.headers.update({"x-api-key": API_KEY})
adapter = HTTPAdapter(pool_connections=20, pool_maxsize=50, max_retries=2)
session.mount('https://', adapter)

w3 = Web3(Web3.HTTPProvider(RPC_URL, session=session))
# Required for Polygon PoS extraData validation
w3.middleware_onion.inject(ExtraDataToPOAMiddleware, layer=0)

def test_throughput():
    if not w3.is_connected():
        print("❌ Failed to connect to BlazingNode")
        return

    print(f"⚡ Connected to Polygon Mainnet (Chain ID: {w3.eth.chain_id})")
    
    start = time.perf_counter()
    block = w3.eth.get_block('latest')
    elapsed = (time.perf_counter() - start) * 1000

    print(f"✅ Latest Block: #{block['number']}")
    print(f"📦 Transactions in Block: {len(block['transactions'])}")
    print(f"⏱️ Roundtrip Time: {elapsed:.2f}ms")

if __name__ == "__main__":
    test_throughput()
```
