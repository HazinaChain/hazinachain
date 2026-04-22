# HazinaChain Node Setup Guide

This guide walks you through setting up a full node on HazinaChain (hazinachain-1).

## Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| CPU | 2 cores | 4 cores |
| RAM | 4 GB | 8 GB |
| Storage | 100 GB SSD | 250 GB SSD |
| OS | Ubuntu 20.04+ | Ubuntu 22.04 |
| Go | 1.21+ | 1.21+ |

---

## Step 1 — Install Go

```bash
wget https://go.dev/dl/go1.21.13.linux-amd64.tar.gz
tar -C /usr/local -xzf go1.21.13.linux-amd64.tar.gz
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
source ~/.bashrc
go version
```

---

## Step 2 — Install HazinaChain Binary

```bash
# Clone the repository
git clone https://github.com/hazinachain/hazinachain
cd hazinachain

# Build
make install

# Verify
hazinad version
```

---

## Step 3 — Initialize Node

```bash
hazinad init <YOUR_MONIKER> --chain-id hazinachain-1 --home ~/.hazinachain
```

---

## Step 4 — Download Genesis

```bash
wget https://raw.githubusercontent.com/hazinachain/hazinachain/main/genesis.json \
  -O ~/.hazinachain/config/genesis.json

# Verify genesis hash
sha256sum ~/.hazinachain/config/genesis.json
```

---

## Step 5 — Configure Node

Edit `~/.hazinachain/config/config.toml`:

```toml
# Set minimum gas prices
minimum-gas-prices = "0.001uhzn"

# Disable peer exchange for single node (optional)
pex = false
addr_book_strict = false

# Enable API
[api]
enable = true
address = "tcp://0.0.0.0:1317"
```

---

## Step 6 — Create Systemd Service

```bash
sudo tee /etc/systemd/system/hazinad.service > /dev/null << EOF
[Unit]
Description=HazinaChain Node
After=network.target

[Service]
Type=simple
User=root
ExecStart=/usr/local/bin/hazinad start \
  --home /root/.hazinachain \
  --minimum-gas-prices 0.001ukumi \
  --p2p.laddr tcp://0.0.0.0:26656 \
  --rpc.laddr tcp://0.0.0.0:26657 \
  --api.enable \
  --api.address tcp://0.0.0.0:1317 \
  --consensus.create_empty_blocks=true
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl enable hazinad
sudo systemctl start hazinad
```

---

## Step 7 — Check Node Status

```bash
# Check sync status
hazinad status --home ~/.hazinachain | python3 -m json.tool | grep latest_block_height

# Check logs
journalctl -fu hazinad -n 50
```

---

## Useful Commands

```bash
# Check balance
hazinad query bank balances <address> --node https://rpc.hazinachain.com

# Send tokens
hazinad tx bank send <from> <to> 1000000uhzn --chain-id hazinachain-1 --node https://rpc.hazinachain.com

# Query validators
hazinad query staking validators --node https://rpc.hazinachain.com

# Check node status via RPC
curl https://rpc.hazinachain.com/status | python3 -m json.tool
```

---

## Troubleshooting

**Port already in use:**
```bash
lsof -i :26657
# Kill the process and restart
systemctl restart hazinad
```

**Wrong validator key:**
```bash
# Check your validator address
hazinad tendermint show-address --home ~/.hazinachain

# Check active validator
curl https://rpc.hazinachain.com/validators | python3 -m json.tool
```

**Node stuck / not producing blocks:**
```bash
# Reset validator state only (keeps chain data)
systemctl stop hazinad
cat > ~/.hazinachain/data/priv_validator_state.json << EOF
{"height":"0","round":0,"step":0}
EOF
systemctl start hazinad
```

---

## Support

- Website: https://hazinachain.com
- Explorer: https://explorer.hazinachain.com
- DeFi App: https://hazina.live
