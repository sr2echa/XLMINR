## Key Numeric Parameters

- **Target Price**: 1 DAI = 1 USD
- **Collateralization Ratio**: Varies by asset, typically 150% for ETH, higher for more volatile assets
- **Liquidation Ratio**: Typically 150% for ETH, can be higher for other assets
- **Stability Fee**: Variable, often between 0.5% to 5% annually, adjusted by governance
- **Dai Savings Rate (DSR)**: Variable, can range from 0% to several percent annually
- **Debt Ceiling**: Set per collateral type, e.g., 100 million DAI for ETH
- **Global Debt Ceiling**: Total DAI that can be generated, e.g., 500 million DAI

## Collateral Value Scenarios in the Maker Protocol

### I. When Your Collateral Increases in Value Over Time

Example:
- Initial: 100 ETH collateral at $200/ETH, 10,000 DAI generated (200% collateralization)
- After increase: ETH price at $300/ETH, now 300% collateralized
- Can now generate up to 5,000 more DAI while maintaining 200% collateralization

### II. When the Collateral Remains Stable in Price

- Stability Fee continues to accrue, e.g., 2% annually on generated DAI

### III. When it Loses Value But Not Significantly Below the Liquidation Ratio

Example:
- Initial: 100 ETH at $200/ETH, 10,000 DAI generated (200% collateralization)
- Price drops to $170/ETH, now 170% collateralized
- Liquidation Ratio at 150%: not liquidated, but at higher risk

### IV. When it Loses Value Below the Liquidation Ratio

Liquidation is triggered when collateral value falls below the Liquidation Ratio.

Example:
- 100 ETH at $200/ETH, 10,000 DAI generated
- Liquidation Ratio: 150%
- If ETH price falls below $150, liquidation is triggered

## Auction Mechanisms

### Collateral Auctions

- Triggered when a Vault becomes undercollateralized
- Liquidation Penalty: Typically 13% added to the debt
- Duration: Often set to 6 hours maximum

### Debt Auctions

- Triggered if Collateral Auctions don't cover system debt
- Mint new MKR tokens to cover shortfall
- Lot Size: Often around 250 DAI worth of MKR

### Surplus Auctions

- Triggered when system surplus exceeds a threshold (e.g., 500,000 DAI)
- Burn MKR tokens with the surplus
- Lot Size: Often around 10,000 DAI

## Important Notes

- Stability Fee accrues continuously, compounding annually
- Liquidation can occur instantly if collateral value drops sharply
- Minimum collateral amount: Often around 10,000 DAI worth
- Emergency Shutdown can be triggered if severe market instability occurs
- Oracle price feeds update frequently, often every hour

## Risk Parameters

- Liquidation Ratio: 150%
- Debt Ceiling: 1 billion DAI

Note: These parameters and other parameters like `Dust (minimum DAI generated)`, `Liquidation Penalty`, `Stability Fee` are subject to change through governance votes.
