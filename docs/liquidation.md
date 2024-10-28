# Liquidation

## What are liquidations?
The Dove protocol operates using overcollateralized loans. Users are allowed to borrow (mint) DVD from the protocol by depositing collateral: cryptocurrency worth more, by a significant margin, than the amount deposited. If the market value of the collateral falls below a certain threshold, then the protocol is at risk of the value of the collateral falling below the value of the DVD minted, which would cause the stablecoin, DVD, to be insufficiently backed. To protect against this, the protocol liquidates the position, selling the collateral on the open market before it can drop too far in value.

## How are liquidations implemented?
Liquidations are implemented using Dutch auctions. A Dutch auction is a type of auction that does not require bids. Instead, the price starts high, and falls continuously with time. For example, if you were to hold a Dutch auction for a chair that lasted an hour, the price might start at $200, then go down to $150 after 15 minutes, then down to $100 after 30 minutes, then down to $50 after 45 minutes, and finally fall to $0 at the end of the hour. If you have several participants that all want the chair, they are all incentivized to buy it at the highest price that they are willing to pay, due to the fear of another participant snapping it up.

In the Dove protocol, collateral auctions begin at 150% of the market price, then sweep all the way down to 15% of the market price, where they are declared failed. Liquidation bots have an incentive to buy the collateral and sell it on the open market at the highest price that is profitable, because otherwise another liquidation bot might get there first.

## Is there a fee for being liquidated?
Yes, there is a fee for being liquidated. When a liquidation occurs, the outstanding debt of the Vault is increased by 5%. In situations of extreme market volatility, the liquidation process may not be swift enough to fully repay a Vault's outstanding debt before the value of the collateral diminishes significantly. This results in bad debt for the protocol. The 5% liquidation fee thus acts as an insurance fund, where successful liquidations provide revenue to the protocol to offset any losses from failed liquidations.

## How can I run a liquidation bot?
To run a liquidation bot, you can refer to [this GitHub repository](https://github.com/doveprotocol/liquidator) for an example implementation. There are three main ways to earn rewards through liquidation:

1. Marking Vaults as liquidated: You'll earn 3% of the outstanding debt or 1,000 DVD, whichever is smaller.

2. Participating in Dutch auctions: By converting collateral into DVD on the open market, you can profit from the difference between the auction price and market price.

3. Marking collateral auctions as failed: You'll earn 1% of the outstanding debt or 250 DVD, whichever is smaller.

These rewards come from the Dove protocol treasury and are separate from the liquidation fee. Vaults are always charged a flat 5% liquidation fee, no more, no less, regardless of the bot's earnings.
