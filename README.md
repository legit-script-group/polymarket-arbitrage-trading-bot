# Polymarket Arbitrage Bot

TypeScript bot for Polymarket 5-minute BTC Up/Down markets using the new-member strategy (time + price bands), we get arbitrage positions here. Uses live Polymarket prices for entry/exit. Logs to console and logs.txt. No wallet or API keys required (read-only price/market APIs).

### Example runs (custom strategy)

Example results from running the bot with different sizes (your own strategy and config):

| Starting balance | Per-trade size | Profit (example run) |
|------------------|----------------|----------------------|
| $100             | $10            | ~$40                 |
| $500             | $50            | ~$300                |
| $1,000           | $100           | ~$500                |

Results depend on market conditions, strategy, and config; the bot often logs “Entry window passed, no position” when it doesn’t find a trade in that 5m window.

| Balance $1517 (e.g. $1k + profit) | Balance $817 (example run) |
|----------------------------|-----------------------------------|
| <img width="1003" height="499" alt="Terminal — Balance $817" src="https://github.com/user-attachments/assets/921dd5d1-72d6-4d62-8a72-7b46db1ccd72" /> | <img width="880" height="491" alt="Terminal — Balance $1517" src="https://github.com/user-attachments/assets/22ee0762-d47a-4ff5-9690-9970dc8b6bcf" /> |

## Strategy

- **Entry:** time 25–71s, price 0.14–0.26  
- **Exit:** time 47–267s, min 3s hold; defer sell if bid < 85% entry; force exit after 5 retries or by t=265s  
- 1% fee and 0.5% slippage applied  
- Output: console + `logs.txt`. Press **Ctrl+C** to stop and see final balance, P/L, trades, duration.  
- No wallet or API keys needed (read-only price/market APIs).

## How to Run the Project


### 1. Install dependencies

```bash
npm install
```

### 2. Configure environment

- Copy `.env.example` to `.env` and set:
  - `POLYMARKET_PRIVATE_KEY` — your wallet private key for signing trades
  - `PROXY_WALLET_ADDRESS` (optional) — only if you use a proxy wallet

### 3. Run the bot

**Live trading (recommended for development):**

```bash
npm start
```

This runs the bot with `tsx` so you see logs in real time. You’ll see lines like:

- `Up=X.XX Down=Y.YY` — current market probabilities
- `Balance: $X.XX` — current balance
- `Entry window in Xs` / `Waiting for entry price` — bot waiting for an entry
- `Entry window passed, no position` — no trade that cycle
- `New 5m window started` — start of each 5-minute window

