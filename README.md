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
- `Swing Selection` (default: 0) - Select which complete zigzag swing to use:
  - **0** = Most recent complete swing (HH-HL, HH-LL, LH-LL, LH-HL, HL-HH, HL-LH, LL-HH, or LL-LH)
  - **1** = Previous complete swing
  - **2** = Two swings back
  - **3+** = Any older swing (up to 19 swings back)
- `Show ZigZag Pivot Points` (default: true) - Display HH/HL/LH/LL labels at both ends of selected swing

**Swing Selection Examples:**
- 0 → Most recent complete zigzag swing (default)
- 1 → Previous complete zigzag swing
- 5 → 5 swings back in history
- 10 → 10 swings back in history

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
4. **Swing Selection**: Select a complete zigzag swing using a single index:
   - **Swing 0** = Most recent complete swing (between pivot[0] and pivot[1])
   - **Swing 1** = Previous complete swing (between pivot[1] and pivot[2])
   - **Swing N** = Older swing (between pivot[N] and pivot[N+1])
   - Each swing is a line between two consecutive pivots forming a pattern like HH-HL, LH-LL, etc.
5. **Fibonacci Drawing**: Fibonacci levels are drawn for the selected complete swing
   - P0 (0%) placed at the newer pivot (where swing ends)
   - P1 (100%) placed at the older pivot (where swing starts)
6. **Dynamic Updates**: As new swings form, pivot history shifts and Fibonacci levels update accordingly

## Differences from Original

- **No manual mode**: All swing detection is automatic via ZigZag
- **No lookback setting**: Uses ZigZag parameters instead
- **Embedded logic**: ZigZag algorithm is integrated directly (no library dependency)
- **Single swing selection**: User selects a complete zigzag swing by index (0-19 swings back)
- **Natural swing pairing**: Always draws between two consecutive pivots forming a complete swing
- **Pivot history tracking**: Stores up to 21 pivots with their types (HH, HL, LH, LL)
- **Complete swing analysis**: Each selection represents a full zigzag line (HH-HL, LH-LL, etc.)
- **Live pivot labeling**: Shows both ends of the selected swing with their pattern types

## Usage

1. Add the indicator to your TradingView chart
2. Adjust ZigZag parameters (Depth, Deviation, Backstep) to match your trading timeframe
3. Select which complete swing to use:
   - **Swing Selection**: Enter 0 for most recent, 1 for previous, 2 for older, etc.
   - Default is 0 (most recent complete zigzag swing)
   - Each swing is a complete line between two consecutive pivots
4. Toggle which Fibonacci levels you want to display
5. Customize colors, line styles, and label sizes to match your chart theme
6. The indicator will automatically draw levels for your selected complete swing

## Credits

- Original Fibonacci indicator: φ-based level calculations
- ZigZag algorithm: Based on MT4 ZigZag by @DevLucem (ZigLib)
