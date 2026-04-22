# Become a HazinaChain Validator

## Prerequisites

- A running full node (see [node-setup.md](node-setup.md))
- At least 1 HZN for self-delegation
- Node fully synced

---

## Step 1 — Create Validator Key

```bash
hazinad keys add <validator-name> --home ~/.hazinachain
```

Save the mnemonic securely — it cannot be recovered!

---

## Step 2 — Get HZN Tokens

Get tokens from the faucet: https://faucet.hazinachain.com

Or buy from the ecosystem: https://hazina.live

---

## Step 3 — Create Validator Transaction

```bash
hazinad tx staking create-validator \
  --amount 1000000uhzn \
  --pubkey $(hazinad tendermint show-validator --home ~/.hazinachain) \
  --moniker "<YOUR_VALIDATOR_NAME>" \
  --identity "<KEYBASE_IDENTITY>" \
  --website "https://yourwebsite.com" \
  --details "Your validator description" \
  --chain-id hazinachain-1 \
  --commission-rate 0.05 \
  --commission-max-rate 0.20 \
  --commission-max-change-rate 0.01 \
  --min-self-delegation 1 \
  --gas auto \
  --gas-adjustment 1.4 \
  --fees 500uhzn \
  --from <validator-name> \
  --node https://rpc.hazinachain.com \
  --broadcast-mode block
```

---

## Step 4 — Verify Validator

```bash
hazinad query staking validators --node https://rpc.hazinachain.com
```

---

## Validator Management

```bash
# Edit validator
hazinad tx staking edit-validator \
  --moniker "New Name" \
  --details "New description" \
  --chain-id hazinachain-1 \
  --from <validator-name> \
  --node https://rpc.hazinachain.com

# Unjail validator
hazinad tx slashing unjail \
  --from <validator-name> \
  --chain-id hazinachain-1 \
  --node https://rpc.hazinachain.com

# Withdraw rewards
hazinad tx distribution withdraw-rewards <validator-address> \
  --commission \
  --from <validator-name> \
  --chain-id hazinachain-1 \
  --node https://rpc.hazinachain.com
```
