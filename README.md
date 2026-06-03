# Deriv Smart Trader Pro

AI-powered trading platform for [Deriv.com](https://deriv.com). Runs entirely in your browser — no server, no build step, single HTML file.

---

## Deploy to GitHub Pages

```bash
git init
git add .
git commit -m "v1.7 release"
git branch -M main
git remote add origin https://github.com/<username>/deriv-smart-trader-pro.git
git push -u origin main
```

Then: **Settings → Pages → Source: main / root → Save**

Live at: `https://<username>.github.io/deriv-smart-trader-pro/`

---

## Get Your Deriv API Token

1. Log in at [app.deriv.com](https://app.deriv.com)
2. **Account Settings → API Token → Create new token**
3. Scopes: **Read + Trade + Payments**
4. Paste token into the login screen and click Connect

---

## Features

- Live WebSocket price feed (Deriv API v3)
- Synthetic Indices (24/7), Forex, Crypto, Baskets, Metals
- Rise/Fall and Higher/Lower contracts
- **Barrier offset control** — live constraints from `contracts_for` API, presets at 1/2/5/10/20/50 pips, absolute price display, +/− direction toggle, debounced live payout proposal
- Live payout preview from real Deriv proposal API
- Charts: EMA 5/20, SMA 50, Bollinger Bands, MACD, Awesome Oscillator, RSI
- **1-minute candle panel** — live forming candle + last 5 closed candles, body%, PERFECT indicator
- **AI signal analyser** — multi-factor confluence scoring (EMA, MACD, AO, RSI, price trend)
- **Auto Trader** — 2-stage AI engine, barrier-sign locked direction (see below)
- Open contracts, trade history, win/loss stats, performance chart
- Compact layout — resizable sidebar, chart drag-handle resize
- Light & Dark mode — ☀/🌙 toggle, localStorage persistence, OS preference detection
- Optimised font clarity throughout

---

## Auto Trader — Barrier-Locked 2-Stage Logic (v1.7)

The Auto Trader is **merged with the barrier offset panel**. You set your barrier manually first, then enable Auto Trade. The barrier sign determines which direction the auto trader is allowed to execute.

### Barrier sign → locked trade direction

| Barrier sign | Auto Trade executes | Why |
|---|---|---|
| `+` (above spot) | **LOWER only** | Price must finish below the barrier to win |
| `−` (below spot) | **HIGHER only** | Price must finish above the barrier to win |

### How to use

1. Switch to **Higher/Lower** contract type
2. Set your **barrier offset** using the presets or manual input
3. Set the **+/−** sign to define your entry direction
4. Set your **stake** and **duration**
5. Click **Auto Trade** — the locked direction is shown in the status bar
6. The engine watches for your barrier-locked direction only

### Execution stages

```
Stage 1 — ARM  (button turns amber)
  AI signal ≥ 80% confidence in the barrier-locked direction
  → Status: "STAGE 2 — waiting"

Stage 2 — FIRE  (trade executes immediately)
  Same direction + AI confidence = 100%
  AND last closed 1m candle is PERFECT (body ≥70%, wicks ≤15%)
  AND candle direction matches: bear candle for LOWER, bull candle for HIGHER
  → Cooldown until next 1m candle closes
```

### Guard rails

| Event | Behaviour |
|---|---|
| Barrier sign toggled while armed | Auto-disarms with warning toast |
| Contract type switched to Rise/Fall | Auto trader disables itself |
| Enabled while in Rise/Fall mode | Error toast — blocked |
| Enabled with barrier offset = 0 | Error toast — blocked |
| Signal direction ≠ barrier-locked direction | Silently ignored |
| Direction flips between Stage 1 and 2 | Disarms with warning toast |

### Button states

| State | Colour | Meaning |
|---|---|---|
| OFF | Grey | Disabled |
| Watching | Green pulse | ON — watching for ≥80% signal in locked direction |
| Armed | Amber pulse | Stage 1 hit — waiting for 100% + perfect 1m candle |

---

## Layout (v1.7)

```
┌──────────────────────────────────────────────────────────────────┐
│  DSP │ ticker tape ··············· │ Bal │ ID │ ● │ ☀ │ Logout  │
├──────────┬────────────────────────────────────┬──────────────────┤
│ Market   │  [Indicators toolbar]              │ Open/History     │
│ Contract │  ┌──────────────────────┬────────┐ │ Stats/AI tabs    │
│ Duration │  │  Main Price Chart    │ 1m ▼   │ │                  │
│ Barrier  │  │                      │ candle │ │                  │
│  +/− set │  ├──── drag handle ─────┴────────┤ │                  │
│ Stake    │  │ MACD │ AO │ RSI               │ │                  │
│ Preview  │  └───────────────────────────────┘ │                  │
│ ──────── │  [⬡ Signal bar + Analyse btn]      │                  │
│ ▲ Higher │                                    │                  │
│ ▼ Lower  │                                    │                  │
│ ──────── │                                    │                  │
│ ⬡ AUTO  │                                    │                  │
│ [status] │                                    │                  │
└──────────┴────────────────────────────────────┴──────────────────┘
     ↑
  drag right edge to resize (180–360px)
```

---

## Bug Fix / Change History

| Version | Change |
|---|---|
| v1.7 | Auto Trader merged with barrier offset — barrier sign locks the execution direction |
| v1.7 | `+` barrier → LOWER only; `−` barrier → HIGHER only |
| v1.7 | Barrier sign toggle while armed → disarms with warning |
| v1.7 | Switching to Rise/Fall mode → auto trader disables itself |
| v1.7 | `updateBarrierUI` refreshes auto-trader status on every barrier change |
| v1.6 | Auto Trader — 2-stage AI execution engine (80%→100% confidence + perfect 1m candle) |
| v1.6 | 1-minute candle panel beside main chart — live forming candle, 5 history bars, body%, PERFECT indicator |
| v1.5 | Font clarity overhaul across all UI zones |
| v1.5 | Light & dark mode, localStorage persistence, OS preference detection |
| v1.4 | Compact layout: fixed topbar, resizable sidebar, chart drag handle, ticker tape |
| v1.3 | Higher/Lower barrier offset panel with live `contracts_for` API constraints |
| v1.3 | Live payout preview from real Deriv proposal API |
| v1.2 | Fixed SyntaxError, missing handleProposal, stale closure, tick subscription |

---

## Disclaimer

Educational and personal use only. Trading involves significant risk of loss. AI signals and the Auto Trader do not guarantee profit. Always test on a demo account first.

## License

MIT
