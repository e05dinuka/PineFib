# Fibonacci with ZigZag Indicator

This Pine Script indicator combines Fibonacci retracement/extension levels with ZigZag swing detection.

## Features

### ZigZag Integration
- **Automatic swing point detection** using MT4-style ZigZag algorithm
- Identifies HH (Higher High), HL (Higher Low), LH (Lower High), LL (Lower Low) patterns
- Configurable parameters: Depth, Deviation, Backstep

### Fibonacci Levels
- Draws Fibonacci levels based on the most recent two ZigZag pivot points
- P0 (0%) and P1 (100%) are automatically set from the last swing
- Supports all φ-based levels including:
  - Retracements: 23.6%, 38.2%, 50%, 61.8%, 78.6%, 88.6%
  - Extensions: 123.6%, 127.2%, 138.2%, 161.8%, 261.8%, 361.8%, 423.6%
  - Negative mirrors: all levels below 0%

### Configuration Options

**ZigZag Settings:**
- `Depth` (default: 12) - Lookback period for swing detection
- `Deviation` (default: 5) - Minimum price movement in ticks
- `Backstep` (default: 2) - Minimum bars between pivots
- `Show ZigZag Pivot Points` - Display HH/HL/LH/LL labels

**Fibonacci Level Visibility:**
- Toggle retracements (0-100%)
- Toggle positive extensions (>100%)
- Toggle negative mirrors (<0%)
- Toggle deep levels (78.6%, 88.6%, √φ)
- Toggle midpoint (50%)
- Toggle 361.8% level

## How It Works

1. **ZigZag Detection**: The indicator continuously monitors price swings using the embedded ZigZag algorithm
2. **Pivot Identification**: When a new swing is confirmed, it identifies the pattern type (HH, HL, LH, LL)
3. **Fibonacci Drawing**: Fibonacci levels are drawn between the last two confirmed pivot points (z1 and z2)
4. **Dynamic Updates**: As new swings form, the Fibonacci levels automatically adjust

## Differences from Original

- **No manual mode**: All swing detection is automatic via ZigZag
- **No lookback setting**: Uses ZigZag parameters instead
- **Embedded logic**: ZigZag algorithm is integrated directly (no library dependency)
- **Live pivot tracking**: Shows the most recent swing pattern type

## Usage

1. Add the indicator to your TradingView chart
2. Adjust ZigZag parameters (Depth, Deviation, Backstep) to match your trading timeframe
3. Toggle which Fibonacci levels you want to display
4. The indicator will automatically draw levels between recent swing points

## Credits

- Original Fibonacci indicator: φ-based level calculations
- ZigZag algorithm: Based on MT4 ZigZag by @DevLucem (ZigLib)
