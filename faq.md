---
description: Frequently asked questions about RAI and GEB
---

# FAQ

### What is TAI?

TAI is an ETH backed stable asset with a [managed float regime](https://en.wikipedia.org/wiki/Managed\_float\_regime). The TAIUSD exchange rate is determined by supply and demand while the protocol that issues RAI tries to stabilize its price by constantly de or revaluing it.

The supply and demand mechanic plays out between two parties: SAFE users (those who generate RAI with their ETH) and RAI holders.

Compared to protocols that try to defend a [fixed exchange rate](https://www.investopedia.com/terms/f/fixedexchangerate.asp) between their native stable asset (pegged coin) and fiat (DAI/USD, sUSD/USD etc), RAI's monetary policy offers a couple of advantages:

* Flexibility: the protocol can devalue or revalue RAI in response to changes in RAI's market price. This process transfers value between SAFE users and RAI holders and incentivizes both parties to bring the market price back to a target chosen by the protocol. The mechanism is similar to countries [devaluing](https://www.investopedia.com/terms/d/devaluation.asp) or [revaluing](https://www.investopedia.com/terms/r/revaluation.asp) their currencies in order to combat a trade imbalance. The "trade imbalance" in RAI's case happens between RAI and SAFE users
* Discretion: the protocol itself is free to change the target exchange rate to its own advantage. It can attract or repel capital whenever it wants.

At the same time, a managed float can cause uncertainty due to the fact that the price varies day by day.

### How does RAI work/behave?

The long term price trajectory of RAI is determined by the demand for ETH leverage. RAI tends to appreciate if SAFE users deleverage and/or RAI users long and it depreciates in case SAFE users leverage and/or RAI users short.

To better understand how RAI behaves, we need to analyze its monetary policy which is made out of four elements:

* Redemption price: this is the price that the protocol wants RAI to have on the secondary market (e.g on Uniswap). The redemption price is used by SAFE users to mint RAI against ETH and it is also used during Global Settlement in order to allow both SAFE and RAI users to redeem collateral from the system. The redemption price almost always floats and it does not target any specific peg.
* Market price: this is the price that RAI is traded at on the secondary market (on exchanges).
* Redemption rate: this is the rate at which RAI is being devalued or revalued. The process of devaluing/revaluing RAI consists in the redemption rate changing the redemption price.
* Global Settlement: settlement consists in shutting down the protocol and allowing both SAFE and RAI users to redeem collateral from the system. Settlement uses the redemption (and not the market) price to calculate how much collateral can be redeemed by each user.

Let's walk through an example of how RAI is revalued in case of ETH capital inflow (aka people are bullish on ETH):

* At time T1: ETH price is $500, RAI's market and redemption prices are both $5
* At time T2: ETH price surges to $1000. RAI SAFE users suddenly have more borrowing power and generate more RAI against their collateral. SAFE users sell RAI on the secondary market (Uniswap), causing RAI's market price to crash to $4.
* At time T3: ETH remains at $1000 and RAI's market price is still $4. The system wants the market price to get close to the redemption price. In order to eliminate the imbalance between the market/redemption prices, the system starts to revalue RAI. Revaluing consists in setting a positive redemption rate which makes the redemption price grow every second.
* At time T4: ETH remains at $1000. RAI's redemption price is now $5.1. SAFE users are starting to realize that they can now borrow less RAI per one ETH, they can redeem less ETH during Settlement (because RAI is now more expensive) and that it will be more expensive to close their SAFE once the market price follows the redemption price. At the same time, RAI holders are starting to realize that they can redeem more and more ETH during settlement
* At time T5: ETH remains at $1000. RAI's redemption price is now $5.2. RAI's market price surged to $5.2 as a result of SAFE users buying RAI in order to close their positions as soon as possible instead of later on when RAI is more expensive

When RAI is devalued (in case of ETH capital outflow), the opposite thing happens:

* SAFE users realize that they can mint more RAI against their ETH and that they will be able to buy cheap RAI once the market price tanks
* Token holders realize that they can redeem less ETH during Settlement and they need to short RAI

### Is RAI a rebase token?

No. The protocol doesn't change the amount of tokens you have. Rather, it changes the target price that the protocol wants RAI to have on exchanges.

### Why would I hold RAI when the system devalues the token?

This is exactly what the system wants you to ask yourself when it charges a negative redemption rate. The system is trying to incentivize RAI holders to sell and bring the market price down and close to the redemption price.

### Isn't RAI growth bounded by ETH growth?

Short answer: yes. Nevertheless, we decided to build a pure ETH system for several reasons:

* Social scalability: we believe the most successful DeFi protocols will be the ones that act as a trust minimized operating system. You can build on top of them without the fear that the rules will drastically change and break your application. For this reason we also want to progressively remove control over RAI.
* Simplicity: it is easier to explain RAI's behaviour in contrast to ETH as opposed to a basket of assets.
* Proof of concept: a system backed by a single collateral type is easier to manage than a multi-collateral one. It allows us to test our hypotheses without layering extra risk and overhead

### Can you summarize the behavior of the RAI redemption rate?

1. When RAI's market price > redemption price for a sustained period of time, the redemption rate will become negative
2. When RAI's market price < redemption price for a sustained period of time, the redemption rate will become positive
3. When RAI's market price = redemption price for a sustained period of time, the redemption rate will settle at a steady state (that may be non zero)

### What is the difference between the redemption rate and the borrow rate?

A system like RAI has two types of rates:

* The borrow rate which is an interest rate charged on open SAFEs. The borrow rate will usually be fixed or bounded
* The redemption rate: this is the rate at which RAI (or RAI-like assets) are devalued or revalued

### Why would I want to mint RAI?

* Getting paid for opening and managing SAFEs: when RAI is devalued, SAFE users are "paid" because the value of their debt shrinks compared to the value of their collateral
* Capped borrow rate: in the long run, RAI will have a capped (and small) borrow rate which makes the cost of maintaining a SAFE more predictable. Governance can, in theory, set the borrow rate to 0% although this prevents the system from accruing surplus that's [used to incentivize keepers](https://docs.reflexer.finance/system-contracts/sustainability-module/stability-fee-treasury) to update core components such as oracles and the PID. A 0% borrow rate would also prevent the protocol from building a surplus buffer meant to settle bad debt that couldn't be covered by collateral auctions
* Insurance for SAFEs: in the long run we can allow SAFE users to attach a wide variety of insurance contracts meant to protect their positions against liquidation
* No exposure to assets with counterparty risk: RAI will only be backed by ETH. Borrowers are not exposed to riskier crypto assets or real world collateral
* Superior collateral factors: as we improve the efficiency of our [collateral auctions](https://docs.reflexer.finance/system-contracts/auction-module/fixed-discount-collateral-auction-house) and add insurance contracts for SAFEs, we can lower the collateral requirements for borrowing RAI

### What are RAI's use-cases?

The following is a non-exhaustive list of use-cases we envision for RAI:

* Portfolio diversification: RAI offers dampened exposure to ETH's price moves
* DeFi collateral: RAI can be used as an ETH supplement or alternative collateral in DeFi protocols due to the fact that it dampens ether's price moves and gives users more time to react to market shifts
* DAO reserve asset: DAOs can keep RAI on their balance sheet and get exposure to ETH without being affected by its full market swings

### Will RAI always return to the same initial value/peg?

RAI is not designed to be pegged to anything, so it may never return to the same value it started at. Similar to many fiat currencies (EUR, GBP etc), RAI will float around, being influenced by market forces (supply & demand) and by the incentives that the PID controller offers to SAFE users and RAI holders.
