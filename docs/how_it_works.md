# How It Works
Traditional, centralized stablecoins like USDC and USDT are typically backed by an equivalent amount of USD in reserve. In contrast, the Dove protocol's decentralized stablecoin, DVD, is backed by cryptocurrency collateral whose value in USD exceeds the number of DVD in circulation. This is achieved through collateralized debt positions (CDPs) called Vaults.

The following is a technical explanation of the economic incentives that allow DVD, a decentralized stablecoin, to exist and maintain its $1 peg. The other sections may be more helpful to a person who only wishes to use the protocol.

## How Vaults work

1. **Depositing collateral**: A user deposits cryptocurrency like SOL into a Vault as collateral. The collateral's value must be higher than the amount of DVD the user wants to generate.

2. **Generating DVD**: The user can generate DVD based on their deposited collateral's value, up to a limit set by governance. For example, if the limit is 80% and the user deposited $1,000 worth of collateral, they could generate up to 800 DVD.

3. **Interest accumulation**: The Vault accumulates interest based on the amount of DVD generated. The interest rate is set by governance. This interest compounds continuously, increasing the Vault's debt and providing revenue for the protocol.

4. **Repaying DVD**: To withdraw their collateral, the user must repay the DVD they generated plus the accumulated interest. This burns the returned DVD. If the user wants to withdraw only part of their collateral, they can repay a portion of the generated DVD.

5. **Liquidation**: If the collateral's value falls enough to push the Vault's collateral ratio below the required minimum, the Vault is considered undercollateralized.

   To protect the system's solvency, undercollateralized Vaults are liquidated. The protocol sells the collateral to repay the DVD debt and a liquidation penalty. Any remaining collateral is returned to the Vault owner.

## Maintaining long-term stability

DVD maintains a market price near $1 through two sets of mechanisms: one that pushes the price to $1 or above, and another that pulls it back down when it exceeds $1.

### Pushing to $1 or higher

1. **Inherent value from collateral redemption**: DVD tokens have inherent value because they are required to retrieve deposited collateral from Vaults. This creates natural demand for DVD. For example, let's say a user deposits $1,000 worth of collateral into a Vault, and generates 800 DVD tokens against this collateral. To get their $1,000 of collateral back, they must return 800 DVD. This makes each DVD effectively worth $1.25 ($1,000 / 800) to the user. So, the need to repay DVD to access valuable collateral gives DVD inherent value, driving demand.

2. **Vault interest rates**: Vaults accrue interest on borrowed DVD at a rate set by governance. Higher rates increase the incentive to repay debt and avoid liquidation, driving DVD demand.

3. **Savings rates**: Users can earn interest on DVD by locking it in Savings. Higher savings rates make holding DVD more attractive, increasing demand.

### Pulling back to $1

If DVD's price climbs substantially above $1, governance can vote to:

1. **Lower Vault interest rates**: This reduces the cost of borrowing DVD and the urgency to repay debt, increasing DVD supply and decreasing demand.

2. **Reduce Savings rates**: Lower Savings rates make holding DVD less attractive, encouraging users to withdraw and sell, increasing supply and reducing demand.

## Ensuring short-term stability

Stability Modules are liquidity pools that let users trade DVD for blue-chip stablecoins like USDC or USDT at a 1:1 ratio without fees. When a user trades a stablecoin for DVD, new DVD is minted. When they trade DVD for a stablecoin, the DVD is burned.

Stability Modules create an arbitrage opportunity that incentivizes traders to buy DVD when its price falls below $1 and sell when its price exceeds $1. This keeps DVD near its $1 target even during brief periods of volatility.

To limit the protocol's exposure in case of a stablecoin losing its peg, governance sets a ceiling on the amount of DVD that can be minted using Stability Modules, typically no more than 0.5% to 1% of the circulating DVD supply.
