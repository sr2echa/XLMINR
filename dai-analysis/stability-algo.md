# MakerDAO's DAI Stability Algorithm

## Overview

MakerDAO employs a sophisticated system to maintain DAI's peg to 1 USD, despite being overcollateralized. This document outlines the key mechanisms used to achieve this stability.

## Core Mechanisms

### 1. Overcollateralization:
While DAI is overcollateralized, this alone doesn't keep its price at $1. It primarily ensures there's always enough backing value for DAI.

### 2. Target Rate Feedback Mechanism (TRFM):
This is the primary algorithm for maintaining DAI's peg:

   **a)** `When DAI price > $1:`
   - The system decreases the Dai Savings Rate (DSR)
   - This reduces demand for holding DAI
   - It also increases the Stability Fee
   - This makes it more expensive to generate DAI, reducing supply
   - These actions put downward pressure on the DAI price

   **b)** `When DAI price < $1:`
   - The system increases the DSR
   - This increases demand for holding DAI
   - It also decreases the Stability Fee
   - This makes it cheaper to generate DAI, increasing supply
   - These actions put upward pressure on the DAI price

### 3. Stability Fee Adjustments:
- MakerDAO governance can vote to adjust the Stability Fee
- Higher fees make DAI generation more expensive, reducing supply
- Lower fees make DAI generation cheaper, increasing supply

### 4. Debt Ceilings:
- Each collateral type has a debt ceiling
- This limits how much DAI can be generated, preventing oversupply

### 5. PSM (Peg Stability Module):
- Allows users to swap certain stablecoins (like USDC) for DAI at a 1:1 ratio
- This provides a direct arbitrage mechanism to keep DAI close to $1

### 6. Automatic Liquidations:
- If collateral value drops, positions are automatically liquidated
- This ensures DAI remains adequately collateralized, maintaining trust and stability

### 7. Emergency Shutdown:
- In extreme cases, the system can be shut down
- This allows DAI holders to claim collateral at the target price of $1

### 8. Market Forces and Arbitrage:
- If `DAI > $1` , users are incentivized to generate more DAI (by depositing collateral) and sell it
- If `DAI < $1` , users are incentivized to buy DAI and use it to repay loans, reducing supply

---
The combination of these mechanisms, especially the TRFM, allows for dynamic adjustments to keep DAI as close to $1 as possible, despite being overcollateralized. The system relies on both algorithmic responses and human governance to maintain stability.
