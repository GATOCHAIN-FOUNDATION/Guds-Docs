# Token Swap System Documentation

## Overview
An automated system that maintains price parity between USDT and GUDS tokens on the Binance Smart Chain through programmatic swaps.

## System Architecture

### Core Components
- Express.js server
- Ethers.js for blockchain interaction 
- Smart contracts for USDT, GUDS, and swap functionality
- Automated monitoring system

### Contract Integrations
- Swap Contract
- USDT Contract
- GUDS Contract

## Key Features

### Token Approval
- Separate approval functions for USDT and GUDS tokens
- Uses maximum allowance (MaxUint256)
- Implements gas price optimization with 2x buffer

### Reserve Monitoring
- Checks token reserves every 10 seconds
- Calculates price ratios between USDT and GUDS
- Formats values to 18 decimal places for accurate comparison

### Automated Swapping Logic
1. **Parity Check**
   - Compares USDT and GUDS reserves to 10 decimal places
   - Triggers swap if imbalance detected

2. **Swap Execution**
   - If USDT < GUDS: Executes swapTokenAToB
   - If GUDS < USDT: Executes swapTokenBToA
   - Swap amount = difference/2 to maintain balance

### Error Handling
- Gas limit errors
- Insufficient allowance detection
- Private key validation
- Generic error capture

## Web Interface
- Real-time console output display
- Black background theme
- Scrollable pre-formatted text output
- Auto-refreshing status updates

## Configuration
- Environment Variables:
  - PRIVATE_KEY: Wallet private key
  - PORT: Server port (default: 5000)
- RPC Provider: BSC Mainnet (bsc-dataseed.binance.org)

## Security Considerations
- Private key management via environment variables
- Gas price optimization to prevent transaction failures
- Double approval protection with MaxUint256

## Monitoring
- Real-time reserve tracking
- Price ratio calculations
- Timestamp logging for all operations
- Console output history (last 60 lines)
