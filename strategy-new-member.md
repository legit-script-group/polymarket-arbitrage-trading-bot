# Strategy inferred from address activity (no code comparison)

**Source:** On-chain/API activity for the address only.

## Universe
- **Markets:** Bitcoin Up or Down, 5-minute windows only.
- **Window length:** 300 seconds (5 min) from market start to resolution.

## Buy and sell depend on BOTH time and price

Decisions are conditional on **current time in the window** and **current share price** (0–1), not on time alone.

---

## When they BUY (time + price)

**Time (seconds after market start):**
- 10th–90th: **25s–71s** (median **51s**). First buy in window: up to **~131s**.
- They enter early in the window; bulk of entries **~39s–65s**.

**Price (of the side they buy):**
- 10th–90th: **0.14–0.26** (median **0.21**).
- Min observed **0.03**, max **~0.26**.
- They buy when the side is **cheap** (avoid paying above ~0.26).

**Entry rule (to follow):** Buy when **time is in [25s, 71s]** (or up to ~131s) **and** **price is in [0.14, 0.26]** (or up to ~0.26). I.e. enter early in the window when the chosen outcome is trading at low price.

---

## When they SELL (time + price)

**Time (seconds after market start):**
- 10th–90th: **47s–119s** (median **79s**). Last sell in window up to **~267s**.
- They do not hold to resolution (300s).

**Price (at which they sell):**
- 10th–90th: **0.11–0.43** (median **0.25**).
- Full range **0.01–0.84** → they sell both at low prices (cut loss) and high prices (take profit).

**Exit rule (to follow):** Sell when **time is in [47s, 119s]** (or up to ~267s) **and** **price** has moved into a level they accept: from **~0.11** (cut loss) up to **~0.43** (take profit), with median **~0.25**. Exact exit depends on current price, not only time.

---

## Flow
- **Entry:** Buy one side (Up or Down) when **time** is in the entry band (e.g. **25s–71s** after start) **and** that side’s **price** is in the entry band (e.g. **0.14–0.26**).
- **Exit:** Sell when **time** is in the exit band (e.g. **47s–119s** or up to **~267s**) **and** **price** is at an acceptable level (from **~0.11** to **~0.43+**; take profit or cut loss).
- **Both sides:** Trade Up and Down across windows depending on which side meets the time+price conditions.

## Sizing
- Variable size per trade: from ~5 to ~115+ shares.
- Recurring sizes: ~24, ~38, ~62 (suggest fixed or tiered size per trade).

## Price behavior
- Sells at a wide price range (e.g. ~0.09–0.63).
- Will exit at both low and high prices → takes profits and cuts losses in the book.

## Summary (to follow)
1. Trade only BTC 5m Up/Down.
2. One directional position per window (Up or Down).
3. Always exit by selling before the window ends; do not hold to resolution.
4. Use tiered or fixed position sizes (e.g. ~24 / ~38 / ~62).
5. No obligation to trade every window; directional view per window.
