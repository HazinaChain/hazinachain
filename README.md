# HazinaChain — The Treasury Blockchain

<p align="center">
  <img src="assets/logo-256.png" alt="HazinaChain Logo" width="120"/>
</p>

<p align="center">
  <a href="https://hazinachain.com">Website</a> •
  <a href="https://explorer.hazinachain.com">Explorer</a> •
  <a href="https://hazina.live">Hazina DeFi</a> •
  <a href="https://faucet.hazinachain.com">Faucet</a> •
  <a href="https://rpc.hazinachain.com">RPC</a> •
  <a href="https://api.hazinachain.com">API</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Chain_ID-hazinachain--1-emerald?style=flat-square"/>
  <img src="https://img.shields.io/badge/SDK-Cosmos_v0.47-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/Consensus-CometBFT_v0.37-green?style=flat-square"/>
  <img src="https://img.shields.io/badge/Status-Live-brightgreen?style=flat-square"/>
</p>

---

## Overview

HazinaChain is a Cosmos SDK Layer 1 blockchain purpose-built for the **Hazina DeFi gaming ecosystem**. The name comes from *"Hazina ya Kweli"* — Swahili for *"true treasure"* — reflecting the platform's mission to create real, verifiable value for its community.

**Key features:**
- ⚡ Fast finality (~5s block time with CometBFT)
- 💎 Native HZN token economy (staking, governance, rewards)
- 🎮 Purpose-built for provably fair DeFi gaming
- 🔗 Cosmos SDK v0.47 — IBC-ready
- 🛡 Proof of Stake consensus

---

## Network Info

| Parameter | Value |
|-----------|-------|
| Chain ID | `hazinachain-1` |
| Token | `HZN` |
| Base Denom | `uhzn` (1 HZN = 1,000,000 uhzn) |
| Secondary Token | `KUMI` (`ukumi`) |
| Bech32 Prefix | `hazina` |
| Block Time | ~5 seconds |
| Inflation | 13% annually |
| Unbonding Period | 21 days |
| Min Gas Price | `0.001uhzn` |

---

## Endpoints

| Service | URL |
|---------|-----|
| RPC | https://rpc.hazinachain.com |
| REST API | https://api.hazinachain.com |
| Explorer | https://explorer.hazinachain.com |
| Faucet | https://faucet.hazinachain.com |
| Website | https://hazinachain.com |

---

## Add to Keplr Wallet

```javascript
await window.keplr.experimentalSuggestChain({
  chainId: "hazinachain-1",
  chainName: "HazinaChain",
  rpc: "https://rpc.hazinachain.com",
  rest: "https://api.hazinachain.com",
  bip44: { coinType: 118 },
  bech32Config: {
    bech32PrefixAccAddr: "hazina",
    bech32PrefixAccPub: "hazinaPub",
    bech32PrefixValAddr: "hazinavaloper",
    bech32PrefixValPub: "hazinavaloperpub",
    bech32PrefixConsAddr: "hazinavalcons",
    bech32PrefixConsPub: "hazinavalconspub"
  },
  currencies: [{ coinDenom: "HZN", coinMinimalDenom: "uhzn", coinDecimals: 6 }],
  feeCurrencies: [{ coinDenom: "HZN", coinMinimalDenom: "uhzn", coinDecimals: 6, gasPriceStep: { low: 0.001, average: 0.0025, high: 0.01 } }],
  stakeCurrency: { coinDenom: "HZN", coinMinimalDenom: "uhzn", coinDecimals: 6 }
});
```

---

## Run a Node

See [docs/node-setup.md](docs/node-setup.md) for full instructions.

**Quick start:**
```bash
# Download binary
wget https://github.com/hazinachain/hazinachain/releases/download/v1.0.0/hazinad-linux-amd64

# Initialize node
hazinad init <your-moniker> --chain-id hazinachain-1

# Download genesis
wget https://raw.githubusercontent.com/hazinachain/hazinachain/main/genesis.json -O ~/.hazinachain/config/genesis.json

# Start node
hazinad start --home ~/.hazinachain --minimum-gas-prices 0.001uhzn
```

---

## Ecosystem

| App | Description | URL |
|-----|-------------|-----|
| Hazina DeFi | 8 provably fair games, MLM referral, staking | https://hazina.live |
| Chain Explorer | Real-time block explorer | https://explorer.hazinachain.com |
| Token Faucet | Get testnet HZN tokens | https://faucet.hazinachain.com |

---

## Repository Structure

```
hazinachain/
├── genesis.json          # Mainnet genesis file
├── assets/               # Logo and brand assets
│   ├── logo-256.png      # Square logo (256x256)
│   ├── logo.svg          # Vector logo
│   └── kumi-256.png      # KUMI token logo
├── hazinachain/          # Chain registry files
│   ├── chain.json        # Chain metadata (Keplr/Mintscan)
│   └── assetlist.json    # Token definitions
├── docs/                 # Documentation
│   ├── node-setup.md     # Run a full node
│   ├── validator.md      # Become a validator
│   └── keplr-add.md      # Add to Keplr wallet
└── README.md
```

---

## License

MIT License — see [LICENSE](LICENSE)

---

<p align="center">Built with ❤️ by the Hazina Team • <a href="https://hazina.live">hazina.live</a></p>
