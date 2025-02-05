# rise-strat
A trading strategy and execution class for RISE SDK. 

# RISE Strategy Documentation

## Overview
The RISE Strategy is a trading strategy implementation that analyzes market signals to make trading decisions. This document explains how the strategy works and how to use it in your trading applications.

## Core Components

### RISEStrategy Class
The main class that handles strategy execution and analysis. It works with a signal generator to create and analyze trading signals.

### Key Features
- Backtesting capabilities
- Trade analysis and metrics calculation
- Position management
- Performance measurement

## How to Use

### 1. Creating a Strategy Instance
```javascript
const strategy = new RISEStrategy(signalGenerator);
```

The strategy requires a signal generator when created. This generator provides market signals that the strategy uses to make decisions.

### 2. Running a Backtest
```javascript
const results = await strategy.backtest(
    'AAPL',                    // Trading symbol
    { length: 14,              // Signal parameters
      threshold: 0.5 },
    '30d'                      // Time range
);
```

### 3. Understanding the Results

The backtest returns two main components:

1. **Trades**: A list of all executed trades, including:
   - Entry price and time
   - Exit price and time
   - Profit/loss
   - Signal direction (BULLISH or BEARISH)

2. **Performance Metrics**:
   - Total number of trades
   - Number of winning trades
   - Number of losing trades
   - Profit factor (total profit divided by total loss)
   - Win rate (percentage of winning trades)

## How It Works

The strategy follows these steps:

1. **Signal Processing**: 
   - Receives market signals from the signal generator
   - Each signal can be BULLISH, BEARISH, or NEUTRAL

2. **Position Management**:
   - Opens a position when receiving a non-NEUTRAL signal
   - Closes the position when receiving an opposite signal
   - Maintains position information during the trade

3. **Performance Analysis**:
   - Tracks all trades and their outcomes
   - Calculates key performance metrics
   - Provides detailed trade history

## Performance Metrics Explained

- **Win Rate**: Shows what percentage of trades were profitable
- **Profit Factor**: Measures strategy efficiency by comparing total profits to total losses
  - Profit Factor > 1: Strategy is profitable
  - Profit Factor < 1: Strategy is losing money
  - Profit Factor = Infinity: Strategy had no losing trades

## Best Practices

1. Always test the strategy with different parameters before live trading
2. Monitor the profit factor and win rate to assess strategy performance
3. Use appropriate time ranges for your trading style
4. Consider transaction costs in your analysis (not included in basic metrics)
