# RATE Mechanics

## 1. Overview

The RATE token has two main functions inside the TAI protocol:

* Backstop mechanism: RATE stakers are the first line of defense in case the TAI protocol goes underwater. The second line of defense is with debt auctions that mint new RATE and auction it in exchange for TAI
* Ungovernance: once governance minimization is finalized, RATE holders will be able to remove control from any remaining components in TAI or, if needed, continue to manage components that may be challenging to ungovern (such as oracles or any other component interacting with other protocols)

## 2. TAI Resource Flow

Before the protocol is governance minimized, TAI will be set up so that stability fees (borrow rate charged to Safes that mint TAI) flow in three places:

* The stability fee treasury, which is a smart contract in charge with paying for oracle updates or any other contract meant to automate TAI parameters
* RATE stakers, which are the first line of defense for the protocol
* Buyback and burn, which is meant to auction TAI in exchange for RATE which is subsequently burned

In the case of RATE stakers, the TAI that accrues for them is auctioned in exchange for RATE. The RATE proceeds from the auction are then sent to the staking pool.\
\
As for buyback and burn, TAI is first accrued in the protocol's balance sheet. Once there's enough TAI in the balance sheet, the protocol can start to auction some of it in exchange for RATE that is then burned.

To visualize all this, you can check the diagram below:

![](.gitbook/assets/untitled-diagram.png)

**NOTE**: TAI only flows to the stability fee treasury, to stakers and in the protocol's balance sheet when the borrow rate charged to Safes is positive. When the borrow rate is negative, the protocol only uses funds from the balance sheet to repay TAI debt from all Safes.

