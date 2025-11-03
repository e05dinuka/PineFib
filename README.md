# Fibonacci with ZigZag Indicator

This Pine Script indicator combines Fibonacci retracement/extension levels with ZigZag swing detection.

## Features

### ZigZag Integration
- **Automatic swing point detection** using MT4-style ZigZag algorithm
- Identifies HH (Higher High), HL (Higher Low), LH (Lower High), LL (Lower Low) patterns
- Configurable parameters: Depth, Deviation, Backstep

### Fibonacci Levels
- Draws Fibonacci levels based on selected ZigZag pivot pairs (see Pivot Selection)
- **P0 (0%)** = Second pivot in time (where the swing ends)
- **P1 (100%)** = First pivot in time (where the swing starts)
- This creates standard Fibonacci retracement behavior:
  - **High → Low swing**: 100% = High (start), 0% = Low (end)
    - Retracements show bounce levels from the low
  - **Low → High swing**: 100% = Low (start), 0% = High (end)
    - Retracements show pullback levels from the high
- Supports all φ-based levels including:
  - Retracements: 23.6%, 38.2%, 50%, 61.8%, 78.6%, 88.6%
  - Extensions: 123.6%, 127.2%, 138.2%, 161.8%, 261.8%, 361.8%, 423.6%
  - Negative mirrors: all levels below 0%

### Configuration Options

**ZigZag Settings:**
- `Depth` (default: 12) - Lookback period for swing detection
- `Deviation` (default: 5) - Minimum price movement in ticks
- `Backstep` (default: 2) - Minimum bars between pivots
- `First Pivot` (default: 1) - Select first pivot by index:
  - **0** = Most recent confirmed pivot
  - **1** = Previous pivot
  - **2** = Two pivots back
  - **3+** = Any older pivot (up to 20 pivots back)
- `Second Pivot` (default: 0) - Select second pivot by index (same system as first)
- `Show ZigZag Pivot Points` (default: true) - Display HH/HL/LH/LL labels for selected pivots

**Pivot Selection Examples:**
- First=1, Second=0 → Draw between previous and most recent pivot (default)
- First=2, Second=1 → Draw between two older pivots
- First=5, Second=3 → Draw between any two pivots in history
- First=0, Second=0 → Draw from most recent to itself (not useful, will show error)

**Fibonacci Level Visibility:**
- Toggle retracements (0-100%)
- Toggle positive extensions (>100%)
- Toggle negative mirrors (<0%)
- Toggle deep levels (78.6%, 88.6%, √φ)
- Toggle midpoint (50%)
- Toggle 361.8% level

**Fibonacci Line Styling:**
- `Fibonacci Line Color` (default: gray) - Color for Fibonacci lines
- `Fibonacci Line Width` (default: 2) - Line thickness for extensions/mirrors
- `Fibonacci Line Transparency` (default: 0) - Transparency for Fibonacci lines (0-100)
- `Retracement Line Width` (default: 1) - Line thickness for 0-100% levels
- `Extend Lines to Right` (default: true) - Extend lines to the right edge

**Fibonacci Label Styling:**
- `Label Text Color` (default: gray) - Color for label text
- `Label Background Color` (default: #f1f1f5) - Background color for labels
- `Label Text Transparency` (default: 0) - Text transparency (0-100)
- `Label Background Transparency` (default: 0) - Background transparency (0-100)
- `Label Size` (default: 1-Tiny) - Size of Fibonacci level labels (1-5)

**Pivot Point Styling:**
- `Bull Pivot Color` (default: lime) - Background color for bullish pivots (HH, LH)
- `Bear Pivot Color` (default: red) - Background color for bearish pivots (LL, HL)
- `Pivot Label Transparency` (default: 0) - Text transparency for white pivot labels (0-100)
- `Pivot Background Transparency` (default: 20) - Background transparency for pivot labels (0-100)
- `Pivot Label Size` (default: 2-Small) - Size of pivot labels (1-5)
- Note: Pivot label text is always white

## How It Works

1. **ZigZag Detection**: The indicator continuously monitors price swings using the embedded ZigZag algorithm
2. **Pivot History**: Stores up to 21 confirmed pivot points in memory (index 0=most recent, 1=previous, etc.)
3. **Pivot Identification**: When a new swing is confirmed, it identifies the pattern type (HH, HL, LH, LL) and stores it
4. **Numeric Pivot Selection**: Select any two pivots using numeric indices:
   - Lower index = more recent pivot
   - Higher index = older pivot
   - Flexible selection allows analyzing any swing in history
5. **Fibonacci Drawing**: Fibonacci levels are drawn between the two selected pivot points
   - P0 (0%) placed at the newer (end) of the two pivots
   - P1 (100%) placed at the older (start) of the two pivots
6. **Dynamic Updates**: As new swings form, pivot history shifts and Fibonacci levels update accordingly

## Differences from Original

- **No manual mode**: All swing detection is automatic via ZigZag
- **No lookback setting**: Uses ZigZag parameters instead
- **Embedded logic**: ZigZag algorithm is integrated directly (no library dependency)
- **Numeric pivot selection**: User can select any two pivots from history (0-20 pivots back)
- **Flexible pairing**: Not limited to adjacent swing pairs - can analyze any two pivots
- **Pivot history tracking**: Stores up to 21 pivots with their types (HH, HL, LH, LL)
- **Live pivot labeling**: Shows the selected pivot pair with their swing pattern types

## Usage

1. Add the indicator to your TradingView chart
2. Adjust ZigZag parameters (Depth, Deviation, Backstep) to match your trading timeframe
3. Select which pivots to use:
   - **First Pivot**: Enter index (0=most recent, 1=previous, 2=older, etc.)
   - **Second Pivot**: Enter index (0=most recent, 1=previous, 2=older, etc.)
   - Tip: Start with defaults (First=1, Second=0) for previous to most recent swing
4. Toggle which Fibonacci levels you want to display
5. Customize colors, line styles, and label sizes to match your chart theme
6. The indicator will automatically draw levels between your selected pivot points

## Credits

- Original Fibonacci indicator: φ-based level calculations
- ZigZag algorithm: Based on MT4 ZigZag by @DevLucem (ZigLib)
