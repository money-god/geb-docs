---
description: Describe the process of liquidation of a Safe.
---

# Liquidations and Auctions

## Overview

When the value of a safe's collateral can no longer safely cover the safe's debt, the safe can be liquidated.  A safe can be liquidated if it's `collateralization ratio`_**,**_ falls below the collateral type's `liquidation ratio`.

$$
collateralization\ ratio = \frac{collateral\ value, $}{debt\ value, $}
$$

`collateral value` is calculated using collateral prices that are delayed a minimum of 1 hour. This gives time for safe owners to react to changing collateral prices.

## Liquidation

When a safe is liquidated, its collateral is seized and put up for auction to sell in order to cover the safe's outstanding debt.  The system currently pays a tip of `liquidation gas costs + 25 TAI` to anyone who liquidates a safe.&#x20;

As a penalty for being liquidated, the system will attempt to raise slightly more than the safe's outstanding debt through the collateral sale.  This extra amount is the `liquidation penalty` and is expressed as a percent of the safe's debt. For example, the liquidation penalty for ETH-A is 1%.



## Auction

To sell the collateral efficiently, the system offers the collateral for sale at a discount and keeps increasing the discount until the collateral is sold. This is a dutch, or `increasing discount`, auction. The system initial offers the collateral for sale at a `minimum discount` and keeps increasing it up to the `maximum discount.` The system linearly increases this discount over a period of 7 days until the collateral is sold. For example,  ETH-A auctions have a minimum discount of 1% and maximum discount of 30%. After 7 days, the collateral will be offered at a 30% discount.



### Collateral Liquidation Parameters:

<table data-full-width="false"><thead><tr><th width="149">Type</th><th width="138">Liq. Ratio, %</th><th width="145" data-type="number">Liq. Penalty, %</th><th>Discount Range, %</th></tr></thead><tbody><tr><td>ETH-A</td><td>145</td><td>2</td><td>1-30</td></tr><tr><td>ETH-B</td><td>130</td><td>3</td><td>1-30</td></tr><tr><td>ETH-C</td><td>170</td><td>1</td><td>1-30</td></tr><tr><td>WSTETH-A</td><td>160</td><td>2</td><td>1-30</td></tr><tr><td>WSTETH-B</td><td>185</td><td>1</td><td>1-30</td></tr><tr><td>WOETH-A</td><td>150</td><td>2</td><td>1-30</td></tr><tr><td>RETH-A</td><td>170</td><td>2</td><td>1-30</td></tr><tr><td>RETH-B</td><td>185</td><td>1</td><td>1-30</td></tr><tr><td>CBETH-A</td><td>170</td><td>2</td><td>1-30</td></tr><tr><td>CBETH-B</td><td>185</td><td>1</td><td>1-30</td></tr><tr><td>RAI-A</td><td>110</td><td>3</td><td>3-30</td></tr></tbody></table>



