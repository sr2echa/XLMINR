# GHO Stablecoin: Algorithms and Mechanisms for Stability

## 1. Over-collateralization and Stability

GHO is designed as an over-collateralized stablecoin, meaning the value of the collateral backing it exceeds the value of GHO tokens in circulation. This provides a buffer against price fluctuations in the collateral assets.

## 2. Available Supply Calculation

The core of GHO's supply management is the Available Supply (AS_GHO) formula:

```math
AS\_GHO\_t = \sum_{n=0}^{N-1} \max(0, CB(n)\_t - LB(n)\_t)
```

Where:
- `N` is the number of Facilitators
- `CB(n)_t` is the Capacity of Bucket `n` at time `t`
- `LB(n)_t` is the Level of Bucket `n` at time `t`

This formula ensures that the total GHO supply never exceeds the sum of all Facilitator capacities.

## 3. Price Stability Mechanisms

### a) Fixed $1 Peg

The Aave Protocol always treats 1 GHO as equal to $1, regardless of market fluctuations. This creates arbitrage opportunities that help maintain the peg:

- **If GHO market price < $1**: Users are incentivized to buy GHO cheaply and repay loans, profiting from the difference.
- **If GHO market price > $1**: Users are incentivized to borrow GHO at $1 and sell at market price for profit.

### b) Interest Rate Adjustment

Aave Governance can adjust the GHO borrow rate (`R_GHO`) to influence supply and demand:

- **Increasing `R_GHO`** discourages borrowing, potentially reducing supply.
- **Decreasing `R_GHO`** encourages borrowing, potentially increasing supply.

## 4. Discount Model

The discount model adds complexity to the interest rate mechanism:

```math
R_GHO_u = 
\begin{cases} 
R_GHO & \text{if } B_{stkAAVE}(u) = 0 \\
R_GHO - R_GHO * R_d & \text{if } B_{stkAAVE} > 0 \land P(u) \leq B_{stkAAVE} * T \\
\frac{R_GHO * P_{nd}(u) + (R_GHO - R_GHO * R_d) * P_d(u)}{P(u)} & \text{if } B_{stkAAVE} > 0 \land P(u) > B_{stkAAVE} * T 
\end{cases}
```

Where:
- `R_GHO_u` is the user's final borrow rate
- `B_stkAAVE(u)` is the user's stkAAVE balance
- `R_d` is the discount rate
- `T` is the discount threshold
- `P(u)` is the user's borrowed principal
- `P_d(u)` is the discounted part of the principal
- `P_nd(u)` is the non-discounted part of the principal

This model allows for fine-tuning of incentives for stkAAVE holders.

## 5. Interest Accumulation and Discount Application

GHO uses a global borrow index (`I`) and user-specific scaled balances (`ScB`) to track interest:

```math
B_debt(u) = ScB(u) * I
```

When applying discounts:

```math
D(u) = R_d * (ScB(u)_{t1} * I_{t2} - ScB(u)_{t1} * I_{t1})
```

```math
ScD(u) = \frac{D(u)}{I_{t2}}
```

```math
B_debt(u)_{t2} = (ScB(u)_{t1} - ScD(u)) * I_{t2}
```

This ensures accurate interest calculation while maintaining the global index.

## 6. Liquidation Mechanism

While not explicitly detailed in the provided whitepaper, over-collateralized systems typically include liquidation mechanisms. If the value of a user's collateral falls below a certain threshold relative to their borrowed GHO, their position can be liquidated. This helps maintain the overall collateralization ratio of the system.

## 7. Facilitator Diversity

By allowing multiple Facilitators with different strategies, GHO can potentially employ various stabilization mechanisms. The Aave DAO can balance Facilitator Bucket capacities to maintain overall system stability.

## Mathematical Proof of Stability

While a rigorous mathematical proof isn't provided in the whitepaper, we can outline a logical argument for GHO's stability:

1. Over-collateralization ensures there's always more value backing GHO than its face value.
2. The fixed $1 peg in Aave creates arbitrage opportunities that push the market price towards $1.
3. Interest rate adjustments allow for supply and demand management.
4. The discount model provides additional levers for fine-tuning supply and demand.
5. Liquidation mechanisms (assumed) protect against undercollateralization.

Given these mechanisms, GHO should tend towards stability at its $1 peg, assuming efficient markets and proper governance decisions. However, extreme market conditions or governance failures could still potentially destabilize the system.

---

This analysis covers the main algorithms and mechanisms described in the whitepaper for stabilizing GHO's value. The system relies on a combination of over-collateralization, fixed pricing within Aave, interest rate adjustments, and arbitrage incentives to maintain its peg.
