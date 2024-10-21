# Tokenized Real World Assets(RWA)

Chainlink Bootcamp 2024

Deployed contract addresses (Avalanche Fuji Testnet)

Real Estate Token: 0x6669343570E86f6D099452aa2bf5ee9777407cA7

Issuer: 0xC4E7ccC6FCc6daaa1Ef319b000b46b9808098c20

RWA Lending: 0x1bb930f4341e61DE7FcF1Cd6C9832Da2a8be71A4

English Auction: 0xB1Dc1872F537f53905F000bc9A582D6Af26388E2

This project leverages **Chainlink** and **Zillow's API** to create a fractionalized real estate token, representing off-chain properties on the blockchain. We use **ERC-1155** for fractional ownership, with cross-chain functionality enabled by **Chainlink CCIP**.
- 该项目利用 Chainlink 和 Zillow 的 API 创建一个细分权益化的房地产代币，代表区块链上的链下财产。我们使用 ERC-1155 进行所有权的细分，并通过 Chainlink CCIP 启用跨链功能。

## Overview

- **Asset Selection**: Real-world properties are tokenized using data sourced from Zillow's API.
- **Token Specification**: An ERC-1155 token enables fractional ownership with unique property metadata (address, year built, lot size, etc.).
- **Blockchain**: Deployed on Avalanche Fuji, with cross-chain capabilities via CCIP for transfers across connected blockchains.
- **Off-chain Integration**: Chainlink Functions fetch and update property data from Zillow daily, ensuring the token reflects the real-world asset.

## Key Smart Contracts

1. **FunctionsSource.sol**

   - Stores the JavaScript code to fetch property metadata from Zillow (address, year built, lot size, etc.).

2. **ERC1155Core.sol**

   - Implements the core ERC-1155 logic, including custom minting functions for the initial issuance and cross-chain transfers.

3. **CrossChainBurnAndMintERC1155.sol**

   - Extends ERC1155Core to support cross-chain transfers using the burn-and-mint mechanism with Chainlink CCIP.

4. **Withdraw.sol**

   - Manages the withdrawal of ERC-20 tokens and native coins (funded with LINK tokens for CCIP fees).

5. **RealEstatePriceDetails.sol**

   - Periodically fetches real estate price data using Chainlink Automation and Functions.

6. **RealEstateToken.sol**

   - Main contract inheriting all functionality from other contracts.

7. **Issuer.sol**

   - Helper contract for minting mock ERC-1155 tokens to simulate real estate issuance.

8. **RWALending.sol**

   - Implements ERC-1155 token lending with initial and liquidation thresholds, slippage protection, and price accuracy via Chainlink Data Feeds.

9. **EnglishAuction.sol**
   - Minimal English auction implementation for auctioning ERC-1155 real estate tokens with native Avalanche Fuji coin bidding.

## Technologies Used

- **Chainlink Functions**: Fetch off-chain property data.
- **Chainlink Data Feeds**: Ensure accurate USDC/USD price conversions.
- **Chainlink Automation**: Automate data updates from Zillow.
- **Zillow API**: Source real estate metadata.

## Usage

- **Minting Tokens**: Use the `Issuer.sol` to mint token on `RealEstateToken.sol` contract representing real-world properties.
- **Cross-Chain Transfers**: Tokens can be transferred across chains via the `CrossChainBurnAndMintERC1155.sol` contract.
- **Real Estate Lending**: Lend tokens through `RWALending.sol` and manage auctions using `EnglishAuction.sol`.
