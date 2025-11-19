# PitchDome LS-OB Swing + Liquidity Sweeps

Custom TradingView indicator written in Pine Script v6 that fuses liquidity sweep detection with order-block visualization. The script is designed to keep charts clean while still surfacing high-value context for swing traders who rely on liquidity grabs and supply/demand reactions.

## Key Capabilities

- Maps bullish and bearish order blocks with configurable extensions, fills, and midlines.
- Tracks liquidity sweeps using pivots, optional swing-size filtering, and dynamic pruning of swept levels.
- Offers independent styling for boxes, midlines, liquidity lines, and highlighted areas.
- Provides alert hooks for new order blocks and liquidity sweeps so strategies can automate entries/exits.

## Inputs Overview

- `Pivot Length`: controls swing sensitivity for both order blocks and volume pivots.
- Order-block controls: extension length, background/border colors, midline style and width, mitigation method.
- Liquidity sweep controls: swing lookback (`Swings`), bullish/bearish colors, line width/style/extend, visibility toggles.
- Liquidity filtering: remove swept liquidity automatically, limit max remembered lines, require a minimum swing-size percentage.

## How It Works

1. **Order Blocks**
   - Detects pivots using `pivotLen` and classifies state (bullish/bearish) based on prior highs/lows.
   - Stores top/bottom/mid coordinates, removes mitigated blocks, then draws boxed regions with midlines using `box.new` and `line.new`.

2. **Liquidity Sweeps**
   - Captures pivot highs/lows across `len` bars, optionally ignoring small swings.
   - Creates extendable lines (and optional filled zones) to represent liquidity pools.
   - Continuously trims lines once price sweeps the corresponding level so only active liquidity remains.

3. **Alerts**
   - `Bullish OB Formed`
   - `Bearish OB Formed`
   - `Liquidity Sweep High`
   - `Liquidity Sweep Low`

## Getting Started

1. Open TradingView, create a new Pine Script editor tab, and paste the contents of `pitchdome_ls_ob_indicator.pine`.
2. Click **Add to chart**; Pine v6 is required.
3. Tune inputs (especially `Pivot Length`, `Swings`, and the mitigation/line styling options) to fit your instrument and timeframe.
4. Enable the alert conditions that match your workflow to get notified when new order blocks or sweeps appear.

## Notes

- The script allocates up to 500 boxes/lines, so avoid enabling every visualization on very low timeframes if performance becomes an issue.
- Because swept liquidity is deleted to prevent clutter, historical sweeps are not retained—disable `Remove Swept Liquidity` if you prefer a static history.

Contributions and variations are welcome—feel free to fork and adapt.

