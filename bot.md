## GUDS Bot Documentation
---

## Overview
The `app.js` file is a Node.js application using the Express framework and the Ethers.js library to interact with Binance Smart Chain (BSC). The application periodically checks the reserves of USDT and GUDS tokens in a liquidity pool and performs swaps when necessary to maintain price parity. The environment variables are managed using `dotenv`.

---

## Dependencies
The script uses the following dependencies:
- **Express**: For handling HTTP routes.
- **Ethers.js**: For blockchain interactions.
- **dotenv**: To manage environment variables securely.

The application connects to the BSC mainnet using an RPC provider URL and interacts with smart contracts defined in a `constant` module.

---

## Key Constants and Variables
- **Smart Contract Details**: The ABI and addresses for the Swap, GUDS, and USDT contracts are imported from the `constant` module.
- **Provider and Wallet**: An Ethers provider is set up to interact with the blockchain, and a wallet is created using a private key from environment variables.
- **Connected Contracts**: The wallet is connected to the respective contracts for interactions.

---

## Logging Mechanism
The default `console.log` function is overridden to capture logs and limit the output to the last 60 lines. This ensures concise logging during execution.

---

## Token Approval Functions
Two asynchronous functions, `ApproveToken1` and `ApproveToken2`, are implemented to grant the Swap contract permission to transfer USDT and GUDS tokens on behalf of the user. The functions include a gas price buffer for transaction reliability.

---

## Reserve Check and Swap Logic
The `checkReservesAndSwap` function:
1. Retrieves the reserves of USDT and GUDS tokens.
2. Calculates their prices and logs the details.
3. Compares reserves to decide if a swap is necessary:
   - If reserves are balanced, no action is taken.
   - If reserves are unbalanced, the function calculates the difference and performs a swap to restore parity.
4. Handles errors such as insufficient gas or token allowance during swaps.

The function is executed every 10 seconds using `setInterval`.

---

## HTTP Endpoint
The application serves a single HTTP route (`/`) that provides a simple HTML interface displaying the current console logs. The page is styled with a black background and white text for a clean, readable look.

---

## Usage
1. **Setup**: Add the private key and other environment variables to a `.env` file.
2. **Run**: Start the application using `node app.js`.
3. **View Logs**: Access the logs via the root route (`/`) in a web browser.

---

## Error Handling
The application accounts for common errors:
- **Gas Fee Issues**: Alerts if insufficient BNB is available for transaction fees.
- **Token Allowance**: Reminds users to approve tokens if permission is not granted.
- **Unexpected Errors**: Provides generic messages for unhandled exceptions.

---

## Periodic Execution
The `checkReservesAndSwap` function runs periodically every 10 seconds to automate the reserve monitoring and swapping process, ensuring liquidity pool parity.

---

This documentation provides a concise understanding of the script's structure and functionality.
