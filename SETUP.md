# Quick Setup — Deriv Smart Trader Pro v1.7

## 1. Get Deriv API token
https://app.deriv.com/account/api-token

Create with scopes: **Read + Trade + Payments**

---

## 2. Push to GitHub

```bash
git init && git add . && git commit -m "v1.7 release" && git branch -M main
git remote add origin https://github.com/<user>/deriv-smart-trader-pro.git
git push -u origin main
```

---

## 3. Enable GitHub Pages

Settings → Pages → Source: **main / root** → Save

URL: `https://<user>.github.io/deriv-smart-trader-pro/`

---

## 4. Login & use

- Paste your API token → **Connect & Authenticate**
- Select a market from the left sidebar (defaults to Volatility 100)
- Use manual trade buttons (**▲ Rise / ▼ Fall** or **▲ Higher / ▼ Lower**) pinned at sidebar bottom

---

## 5. Auto Trader — Step-by-step

The Auto Trader requires **Higher/Lower** contract type and a manually set barrier.

| Step | Action |
|---|---|
| 1 | Switch contract type to **Higher/Lower** |
| 2 | Set your **barrier offset** using presets (1, 2, 5, 10, 20, 50 pips) or manual input |
| 3 | Set the **+/−** sign — `+` locks LOWER trades, `−` locks HIGHER trades |
| 4 | Set your **stake** and **duration** |
| 5 | Click **Auto Trade** — green pulse = watching |
| 6 | Stage 1: AI hits ≥80% confidence in your locked direction → button turns amber |
| 7 | Stage 2: AI hits 100% confidence AND last closed 1m candle is perfect → trade fires |
| 8 | Cooldown until next 1m candle closes, then Stage 1 watching resumes |

**To stop:** click the Auto Trade button again at any time.

### Barrier sign rules

| You set | Auto trades | Because |
|---|---|---|
| `+0.05` | LOWER only | Spot must finish below `price + 0.05` |
| `−0.05` | HIGHER only | Spot must finish above `price − 0.05` |

---

## 6. 1-Minute Candle Panel

Fixed 72px column on the right edge of the main price chart.

- **Current forming candle** — large, highlighted with directional colour
- **Last 5 closed candles** — smaller faded bars for context
- **Info row** — direction (▲ BULL / ▼ BEAR), body%, ✓ PERFECT or ⚬ forming

A candle is **PERFECT** when: body ≥ 70% of total range AND neither wick > 15% of range.

---

## 7. Layout controls

| Control | How |
|---|---|
| Resize sidebar | Drag right edge of left panel |
| Resize chart/sub-charts | Drag handle between main chart and MACD/AO/RSI panels |
| Toggle indicators | Buttons in the indicator toolbar above the chart |
| Force AI re-analysis | Click **⟳ Analyse** in the signal bar |
| Switch theme | Click **☀ / 🌙** in the topbar |

---

## 8. Theme

| Setting | Detail |
|---|---|
| Default | Auto-detects OS `prefers-color-scheme` |
| Dark | Deep charcoal, sky-blue accent, teal/rose signals |
| Light | Clean white, ink-blue accent, emerald/crimson signals |
| Persistence | Saved to `localStorage` |

---

## 9. Troubleshooting

| Problem | Fix |
|---|---|
| Auth failed | Token needs Read + Trade + Payments scopes |
| No prices | Use Synthetic Indices — available 24/7 |
| Barrier panel not showing | Switch to **Higher/Lower** contract type |
| Payout shows `…` | Adjust barrier or stake to refresh proposal |
| Chart blank | Wait 2–5 ticks after selecting a market |
| Auto Trade button blocked | Must be in Higher/Lower mode with barrier offset > 0 |
| Auto trade not firing | Confidence must reach 100% AND last closed 1m candle must be perfect |
| Auto disarmed unexpectedly | Barrier sign was changed — reset and re-enable |
| WebSocket error | Try the alternative Binary server in the login dropdown |
| Theme not saving | Check `localStorage` is not blocked by browser privacy settings |
