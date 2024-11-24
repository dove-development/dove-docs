# How It Works
Traditional stablecoins like USDC and USDT maintain their value through centralized reserves of US dollars. The Dove protocol takes a different approach - its decentralized stablecoin, Dove USD (DVD), is backed by cryptocurrency collateral worth more than the total DVD supply. Users can mint DVD by depositing collateral into smart contracts called Vaults.

The following is a technical explanation of the economic incentives that allow DVD, a decentralized stablecoin, to exist and maintain its target peg. The other sections may be more helpful to a person who only wishes to use the protocol.

## How Vaults work

1. **Depositing collateral**: A user deposits cryptocurrency like SOL into a Vault as collateral. The collateral's value must be higher than the amount of DVD the user wants to generate.

2. **Generating DVD**: The user can generate DVD based on their deposited collateral's value, up to a limit set by governance. For example, if the limit is 80% and the user deposited $1,000 worth of collateral, they could generate up to 800 DVD.

3. **Interest accumulation**: The Vault accumulates interest based on the amount of DVD generated. The interest rate is set by governance. This interest compounds continuously, increasing the Vault's debt and providing revenue for the protocol.

4. **Repaying DVD**: To withdraw their collateral, the user must repay the DVD they generated plus the accumulated interest. This burns the returned DVD. If the user wants to withdraw only part of their collateral, they can repay a portion of the generated DVD.

5. **Liquidation**: If the collateral's value falls enough to push the Vault's collateral ratio below the required minimum, the Vault is considered undercollateralized.

   To protect the system's solvency, undercollateralized Vaults are liquidated. The protocol sells the collateral to repay the DVD debt and a liquidation penalty. Any remaining collateral is returned to the Vault owner.

## DVD's target price

Unlike traditional stablecoins that target a fixed $1 value, DVD has a dynamic target price that appreciates over time. At launch, DVD's target price was 1 USD. This target increases continuously at an interest rate set by the DAO, making DVD a yield-bearing stablecoin. For example, if you bought $1 of DVD and held it for one year where the average interest rate was 7%, the value of your holdings would increase from $1.00 to $1.07.

DVD maintains its target price through a balanced system of economic incentives. These incentives work in two directions: upward pressure mechanisms ensure DVD doesn't fall below its target, while downward pressure mechanisms prevent it from rising too far above. The following sections detail how these mechanisms work together to maintain DVD's stability.

### Pushing to target price or higher

1. **Inherent value from collateral redemption**: DVD tokens have inherent value because they are required to retrieve deposited collateral from Vaults. This creates natural demand for DVD. For example, let's say a user deposits $1,000 worth of collateral into a Vault, and generates 800 DVD tokens against this collateral. To get their $1,000 of collateral back, they must return 800 DVD. This makes each DVD effectively worth $1.25 ($1,000 / 800) to the user. So, the need to repay DVD to access valuable collateral gives DVD inherent value, driving demand.

2. **Vault interest rates**: Vaults accrue interest on borrowed DVD at a rate set by governance. Higher rates increase the incentive to repay debt and avoid liquidation, driving DVD demand.

3. **Savings rates**: Users can earn interest on DVD by locking it in Savings. Higher savings rates make holding DVD more attractive, increasing demand.

### Pulling back to target price

If DVD's price climbs substantially above its target price, governance can vote to:

1. **Lower Vault interest rates**: This reduces the cost of borrowing DVD and the urgency to repay debt, increasing DVD supply and decreasing demand.

2. **Reduce Savings rates**: Lower Savings rates make holding DVD less attractive, encouraging users to withdraw and sell, increasing supply and reducing demand.

## Ensuring short-term stability

Stability Modules are liquidity pools that let users trade DVD for blue-chip stablecoins like USDC or USDT at the target price ratio without fees. When a user trades a stablecoin for DVD, new DVD is minted. When they trade DVD for a stablecoin, the DVD is burned.

Stability Modules create an arbitrage opportunity that incentivizes traders to buy DVD when its price falls below the target price and sell when its price exceeds it. This keeps DVD near its target even during brief periods of volatility.

To limit the protocol's exposure in case of a stablecoin losing its peg, governance sets a ceiling on the amount of DVD that can be minted using Stability Modules, typically no more than 0.5% to 1% of the circulating DVD supply.
