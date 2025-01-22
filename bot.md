## GUDS Bot Documentation
---


## Overview
The `app.js` file is a Node.js application that uses Express and Ethers.js to interact with Binance Smart Chain (BSC). It monitors the reserves of USDT and GUDS tokens in a liquidity pool and performs swaps to maintain price parity. Environment variables are managed using `dotenv`.

---

## Dependencies
The script uses the following dependencies:
- **Express**: Handles HTTP routes.
- **Ethers.js**: Facilitates blockchain interactions.
- **dotenv**: Secures environment variable management.

The application connects to the BSC mainnet using an RPC provider URL and interacts with smart contracts defined in a `constant` module.

---

## Key Constants and Variables
- **Smart Contract Details**: The ABI and addresses for Swap, GUDS, and USDT contracts are imported from the `constant` module.
- **Provider and Wallet**: An Ethers provider interacts with the blockchain, and a wallet is created using a private key from environment variables.
- **Connected Contracts**: The wallet connects to the respective contracts for interactions.

---

## Logging Mechanism
The default `console.log` function is overridden to capture and limit the output to the last 60 lines. This ensures concise logging during execution.

---

## Token Approval Functions
Two asynchronous functions are implemented to grant permission for token transfer:
- **`ApproveToken1`**: Approves the Swap contract to transfer USDT tokens.
- **`ApproveToken2`**: Approves the Swap contract to transfer GUDS tokens.

The functions buffer the gas price to ensure transaction reliability:

Gas Price with Buffer = Current Gas Price} * 2

---

## Reserve Check and Swap Logic
The `checkReservesAndSwap` function operates as follows:

### 1. **Retrieve Reserves**
The function fetches the reserves of USDT and GUDS tokens from the Swap contract:

Reserves (USDT) = reserveToken1

Reserves (GUDS) = reserveToken2


### 2. **Calculate Prices**
The prices of USDT and GUDS tokens relative to each other are computed using the following formulas:


Price of USDT (in GUDS) = Reserves (USDT) / Reserves (GUDS)
Price of GUDS (in USDT) = Reserves (GUDS) / Reserves (USDT)


### 3. **Perform Swap**
- If reserves are balanced:

Reserves (USDT) = Reserves (GUDS)

No action is taken.

- If reserves are unbalanced, the difference is calculated:

Difference in Wei= | Reserves (USDT) - Reserves (GUDS) |

To restore parity, the function performs a swap with half the difference:

Swap Amount = Difference in Wei / 2

The swaps are executed using:
- **`swapTokenAToB`** for swapping USDT to GUDS.
- **`swapTokenBToA`** for swapping GUDS to USDT.

### 4. **Error Handling**
The function addresses the following errors:
- Insufficient BNB for gas fees.
- Tokens not approved for contract use.
- Other unexpected errors.

---

## HTTP Endpoint
The application serves a single HTTP route (`/`), providing a simple HTML interface displaying current logs. The interface is styled for readability with a black background and white text.

---

## Usage
1. **Setup**: Add the private key and other environment variables to a `.env` file.
2. **Run**: Start the application using:
   ```bash
   node app.js
   ```
3. **Monitor**: View logs and reserve details at `http://localhost:<PORT>`.

---

## Periodic Execution
The `checkReservesAndSwap` function runs every 10 seconds using `setInterval`, automating reserve monitoring and swaps.

---

This documentation provides an organized overview of the application's structure, functionality, and mathematical formulas for token pricing and swaps.

<img width="1383" alt="image" src="https://github.com/user-attachments/assets/bc3a47a7-3b66-4a8f-b82d-69f3e7c642e0" />

