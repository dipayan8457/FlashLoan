# FlashLoan Arbitrage Contract

## Overview

This Solidity contract facilitates flash loan-based triangular arbitrage on the Ethereum blockchain. Designed to leverage price differences between assets on PancakeSwap, it aims to generate profits through successive trades within a single transaction block. 

## Aim of the Project

The primary goal of this project is to utilize flash loans to execute profitable triangular arbitrage strategies automatically. By leveraging rapid trades across different decentralized exchanges (DEXs), the contract aims to capitalize on price discrepancies, enabling users to profit without any initial capital outlay.

## Key Terminology

### Decentralized Finance (DeFi)

DeFi refers to a movement that aims to recreate traditional financial systems (like lending and trading) using decentralized technologies, primarily blockchain. DeFi eliminates intermediaries, allowing users to engage in peer-to-peer transactions.

### Flash Loans

Flash loans are uncollateralized loans that must be borrowed and repaid within the same transaction block. They allow users to access large amounts of capital without upfront collateral, making them a powerful tool for arbitrage and other financial strategies.

### PancakeSwap

PancakeSwap is a decentralized exchange (DEX) operating on the Binance Smart Chain (BSC), enabling users to swap various cryptocurrencies without a centralized authority. It utilizes an automated market maker (AMM) model to facilitate trades and liquidity provision.

## Contract Functionality

### `initiateArbitrage`

- **Description**: Initiates the arbitrage by swapping borrowed BUSD for WBNB in the liquidity pool.
- **Parameters**:
  - `_busdBorrow`: Address of the borrowed BUSD token.
  - `_amount`: Amount of BUSD to borrow for the arbitrage.
- **Actions**:
  - Approves BUSD, CROX, and CAKE token spending on the PancakeSwap Router.
  - Identifies the liquidity pool between BUSD and WBNB.
  - Swaps BUSD for WBNB in the liquidity pool, initiating the arbitrage process.

### `pancakeCall`

- **Description**: Executes the arbitrage steps and handles repayment to the flash loan pool.
- **Parameters**:
  - `_sender`: Address initiating the call.
  - `_amount0`: Amount of the first token in the pair.
  - `_amount1`: Amount of the second token in the pair.
  - `_data`: Encoded data containing details for the arbitrage.
- **Actions**:
  - Checks and validates the sender and contract alignment.
  - Decodes the data to retrieve loan details (borrowed token, amount, borrower's address).
  - Executes the series of trades for triangular arbitrage (BUSD → CROX → CAKE → BUSD).
  - Verifies the profitability of the arbitrage.
  - Transfers profits to the initiator and repays the flash loan.

### Other Functions

- `getBalanceOfToken`: Retrieves the contract's balance of a specific token.
- `placeTrade`: Executes token swaps through PancakeSwap based on specified tokens and amounts.
- `checkResult`: A helper function to check if the arbitrage yields profits.

## Usage

1. **Run the contracts in your local code editor using Hardhat.**
2. **Call `initiateArbitrage` with the desired parameters to start the arbitrage process.**
3. The contract will autonomously execute trades and handle repayments.
4. Ensure sufficient liquidity and price differences to yield profitable arbitrage. If you encounter an error stating "Not profitable Arbitrage," find crypto pairs and replace them in the contract that can provide profitable arbitrage.

## Disclaimer

⚠️ Triangular arbitrage involves financial risks. Understanding the contract functionalities, market dynamics, and implications is crucial before using this software.

---
