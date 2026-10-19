# Natural Squares (Gann) for TradingView

A Pine Script v6 indicator that plots Gann **natural squares** (n²) and the in-between Square of Nine levels as horizontal price levels, with automatic price scaling so it works on any instrument: futures, forex, volatility indexes and more.

<img width="1835" height="962" alt="image" src="https://github.com/user-attachments/assets/ffb72bc6-91e9-42b6-8bfd-e76105cda062" />


## What it does

Natural squares are the prices that are perfect squares: 100, 121, 144, 169... Taking the square root of price puts it on the Square of Nine wheel, where every **0.5 step in the root is a 90° move** and every **0.25 step is 45°**. This indicator draws the levels above and below the current price, labels them with their root and angle, and highlights the nearest level on each side.

## Features

- Natural squares (n²) and fractional-root squares at steps of 1, 0.5, 0.25, 0.125 or 0.0625
- **Auto price scaling**, so forex, VIX and low-priced assets get usable level spacing (see below)
- **Square of Nine angle labels** on every level (angle = (root mod 2) × 180°)
- **Angle filter**: show all levels, cardinal only (0/90/180/270), or cardinal + diagonal (45° steps)
- Nearest level above and below price highlighted
- Distance from close in **pips on forex**, points elsewhere
- Optional price, root and angle labels, plus an on-chart readout of the active scale
- Alerts when price crosses a (filtered) square level
- Configurable line width, style, colors and label size

## Why scaling matters

Levels are n², so the gap between neighboring levels grows with the square root of price:

```
spacing ≈ 2 × √(scaled price) × root step   (in scaled units)
```

On NQ at 25,000 the root is about 158, so levels are well spaced. On EURUSD at 1.08 the root is about 1.04, so whole squares sit at 1.0 and 4.0 and the indicator is useless without scaling. The standard Gann fix is to scale price first (EURUSD 1.0850 → 10850), then divide the levels back.

**Auto** mode picks a power of 10 so the scaled price lands in the 10,000–99,999 range (prices already at or above 10,000 are left unscaled). You can also pick a fixed scale or enter a custom one.

> **Note:** angles and roots depend on the scale. EURUSD at x10000 and x1000 give different roots and angles. The scale is part of the method, so the active scale is shown in the top-right corner of the chart.

## Recommended root step

Approximate level spacing at the example prices shown. Pick the step that gives you the density you want.

| Instrument (example price) | Auto scale | Step 1.0 | Step 0.5 | Step 0.25 | Step 0.125 | Step 0.0625 |
|---|---|---|---|---|---|---|
| NQ (25,000) | x1 | ~316 pts | ~158 pts | ~79 pts | ~40 pts | ~20 pts |
| ES (6,000) | x1 | ~155 pts | ~77 pts | ~39 pts | ~19 pts | ~10 pts |
| EURUSD (1.0850) | x10000 | ~208 pips | ~104 pips | ~52 pips | ~26 pips | ~13 pips |
| VIX (20) | x1000 | ~0.28 | ~0.14 | ~0.07 | ~0.035 | ~0.018 |

For intraday scalping, 0.25 or 0.125 is a good starting point. For swing or higher-timeframe use, 0.5 or 1.0.

## Inputs

**Levels**
- **Root step:** spacing between roots (1, 0.5, 0.25, 0.125, 0.0625)
- **Levels each side of price:** how many levels to draw above and below
- **Price scale:** Auto, a fixed power of 10, or Custom
- **Angle filter:** All angles, Cardinal only, or Cardinal + diagonal. Filtered-out levels are not drawn, not highlighted and do not trigger alerts. Needs a root step of 0.5 or smaller to filter beyond 0°/180°

**Colors:** whole-root squares, fractional-root squares, nearest-level highlight

**Style:** line width and style, labels, prices, angles, distance, scale readout, label size

**Alerts:** alert on price crossing a level

## Installation

1. Open the Pine Editor in TradingView.
2. Paste the contents of `natural_squares.pine`.
3. Click **Add to chart**.

To use alerts: enable "Alert when price crosses a square" in the settings, then create a new alert and pick this indicator under Condition.

## Known limitations

- Levels are drawn on the last bar only and extend across the chart. There is no historical level plotting.
- Limited to 200 lines and 200 labels (TradingView allows up to 500 per script).
- Distance in pips assumes the symbol type is reported as forex by TradingView and uses 10 × mintick as one pip.
- Alerts report only the highest level crossed if price jumps across several levels in a single bar.

## Disclaimer

This indicator is a charting tool for educational purposes and is not financial advice. Support/resistance and Gann methods are subjective and have no guaranteed predictive value. Trading involves risk of loss.

## License

MIT. See `LICENSE`.
