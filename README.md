# DrexSmartContracts

This repository contains a simulated Solidity implementation of the Drex Central Bank Digital Currency (CBDC) smart contract. Based on the conceptual architecture of the Brazilian Central Bank's Digital Real, this project utilizes the OpenZeppelin library to provide a robust ERC20 token standard enhanced with critical regulatory features.

**Disclaimer:** This code is for educational and illustrative purposes only. It is not an official implementation and must not be used in a production environment without rigorous auditing and legal compliance.

## Key Features

*   **Minting & Burning:** Authorized accounts can generate or destroy tokens to manage supply.
*   **Access Control:** Role-based security (`MINTER_ROLE`, `BURNER_ROLE`, `PAUSER_ROLE`, `MOVER_ROLE`) ensures strict authorization protocols.
*   **Transaction Freezing:** The contract supports freezing specific balances or entire accounts to comply with regulatory requirements.
*   **Pausable Mechanisms:** Authorized roles can pause and unpause all token transfers globally during security incidents.
*   **Regulatory Compliance:** Overrides standard ERC20 `transfer` and `transferFrom` functions to include custom checks for account status and frozen balances.

## Architecture

The contract inherits from several OpenZeppelin modules:

*   `ERC20`: Standard token functionality.
*   `ERC20Burnable`: Extensions for burning tokens.
*   `AccessControl`: Granular role management.
*   `Pausable`: Emergency stop mechanisms.

## Installation

To run this project locally, you need Node.js and Hardhat.

bash
# Install dependencies
npm install

# Compile contracts
npx hardhat compile

# Run tests
npx hardhat test


## Contract Interface

### Account Management

*   `disableAccount(address account)`: Restricts an address from transferring tokens.
*   `enableAccount(address account)`: Re-enables a restricted address.
*   `authorizedAccount(address account)`: Verifies if an address is currently allowed to transact.

### Balance Management

*   `increaseFrozenBalance(address account, uint256 amount)`: Locks a specific amount of tokens within an account.
*   `decreaseFrozenBalance(address account, uint256 amount)`: Unlocks previously frozen tokens.
*   `frozenBalanceOf(address account)`: Returns the amount of tokens currently locked for an account.

### Token Operations

*   `mint(address to, uint256 amount)`: Creates new tokens (Minter role required).
*   `burn(uint256 amount)`: Destroys tokens from the caller's balance (Burner role required).
*   `pause()`: Halts all transfers (Pauser role required).
*   `unpause()`: Resumes transfers.

## Security Warning

**Do not use this code for financial operations.** This is a simulation. Official CBDC implementations require strict adherence to banking laws and advanced security audits. Always verify contract logic before deployment to the mainnet.