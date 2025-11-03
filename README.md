# Fibonacci with ZigZag Indicator

This Pine Script indicator combines Fibonacci retracement/extension levels with ZigZag swing detection.

## Features

### ZigZag Integration
- **Automatic swing point detection** using MT4-style ZigZag algorithm
- Identifies HH (Higher High), HL (Higher Low), LH (Lower High), LL (Lower Low) patterns
- Configurable parameters: Depth, Deviation, Backstep

### Fibonacci Levels
- Draws Fibonacci levels based on the **previous** two ZigZag pivot points (z0 and z1)
- P0 (0%) and P1 (100%) are automatically set from the completed swing (not the currently forming one)
- Supports all φ-based levels including:
  - Retracements: 23.6%, 38.2%, 50%, 61.8%, 78.6%, 88.6%
  - Extensions: 123.6%, 127.2%, 138.2%, 161.8%, 261.8%, 361.8%, 423.6%
  - Negative mirrors: all levels below 0%

### Configuration Options

**ZigZag Settings:**
- `Depth` (default: 12) - Lookback period for swing detection
- `Deviation` (default: 5) - Minimum price movement in ticks
- `Backstep` (default: 2) - Minimum bars between pivots
- `Pivot Selection` (default: "Previous swing") - Choose which pivot pair to use:
  - **Most recent swing (z2 ↔ z1)** - Uses the last confirmed swing
  - **Previous swing (z1 ↔ z0)** - Uses one swing back (more stable)
  - **Older swing (z0 ↔ z-1)** - Uses two swings back (most stable)
- `Show ZigZag Pivot Points` (default: true) - Display HH/HL/LH/LL labels for selected pivots

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
2. **Pivot Identification**: When a new swing is confirmed, it identifies the pattern type (HH, HL, LH, LL)
3. **Pivot Selection**: Choose which pair of pivots to use for Fibonacci calculation:
   - Most recent, previous, or older swing
   - More recent = more responsive but may repaint
   - Older = more stable and less repainting
4. **Fibonacci Drawing**: Fibonacci levels are drawn between the selected two pivot points
5. **Dynamic Updates**: As new swings form, the Fibonacci levels update based on your pivot selection

## Differences from Original

- **No manual mode**: All swing detection is automatic via ZigZag
- **No lookback setting**: Uses ZigZag parameters instead
- **Embedded logic**: ZigZag algorithm is integrated directly (no library dependency)
- **Pivot selection**: User can choose which swing to use (most recent, previous, or older)
- **Live pivot tracking**: Shows the selected pivot pair with swing pattern types (HH, HL, LH, LL)

## Usage

1. Add the indicator to your TradingView chart
2. Adjust ZigZag parameters (Depth, Deviation, Backstep) to match your trading timeframe
3. Toggle which Fibonacci levels you want to display
4. The indicator will automatically draw levels between recent swing points

## Credits

- Original Fibonacci indicator: φ-based level calculations
- ZigZag algorithm: Based on MT4 ZigZag by @DevLucem (ZigLib)
