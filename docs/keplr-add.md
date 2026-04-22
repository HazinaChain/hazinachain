# Add HazinaChain to Keplr Wallet

## Method 1 — Click to Add (Recommended)

Visit https://hazinachain.com and click **"Add to Keplr"** button.

---

## Method 2 — Manual JavaScript

Open browser console on any page and run:

```javascript
await window.keplr.experimentalSuggestChain({
  chainId: "hazinachain-1",
  chainName: "HazinaChain",
  rpc: "https://rpc.hazinachain.com",
  rest: "https://api.hazinachain.com",
  bip44: {
    coinType: 118
  },
  bech32Config: {
    bech32PrefixAccAddr: "hazina",
    bech32PrefixAccPub: "hazinaPub",
    bech32PrefixValAddr: "hazinavaloper",
    bech32PrefixValPub: "hazinavaloperpub",
    bech32PrefixConsAddr: "hazinavalcons",
    bech32PrefixConsPub: "hazinavalconspub"
  },
  currencies: [
    {
      coinDenom: "HZN",
      coinMinimalDenom: "uhzn",
      coinDecimals: 6,
      coinGeckoId: ""
    }
  ],
  feeCurrencies: [
    {
      coinDenom: "HZN",
      coinMinimalDenom: "uhzn",
      coinDecimals: 6,
      gasPriceStep: {
        low: 0.001,
        average: 0.0025,
        high: 0.01
      }
    }
  ],
  stakeCurrency: {
    coinDenom: "HZN",
    coinMinimalDenom: "uhzn",
    coinDecimals: 6
  }
});
```

---

## Method 3 — Chain Registry (After Listing)

Once HazinaChain is listed on the cosmos/chain-registry, it will appear automatically in Keplr's chain list.

---

## Network Details for Manual Entry

| Field | Value |
|-------|-------|
| Chain ID | hazinachain-1 |
| Chain Name | HazinaChain |
| RPC URL | https://rpc.hazinachain.com |
| REST URL | https://api.hazinachain.com |
| Coin Denom | HZN |
| Coin Minimal Denom | uhzn |
| Coin Decimals | 6 |
| Bech32 Prefix | hazina |
| Coin Type | 118 |
| Gas Low | 0.001 |
| Gas Average | 0.0025 |
| Gas High | 0.01 |
