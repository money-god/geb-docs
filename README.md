---
description: The what and how of the GEB framework
---

# Introduction to GEB

[GEB](https://en.wikipedia.org/wiki/G%C3%B6del,\_Escher,\_Bach) is a framework for deploying systems that can issue [stablecoins](https://medium.com/money-god/stability-without-pegs-8c6a1cbc7fbd). Stablecoins don't look like [this](https://www.coingecko.com/en/coins/usd-coin) (that's a pegged coin), but rather like [this](https://duneanalytics.com/HggqX/Moneygod-TAI). Stablecoins are a great collateral source for other DeFi protocols (compared to ETH or BTC) and are also a store of value with an embedded funding rate.\
\
This documentation is meant to explain all the components behind GEB. Before diving in the docs, we recommend reading our original [whitepaper](https://mirror.xyz/0x01393d9b6dFFce134b6765e9bdd626b258357C37/e0vdmPeoieNaLKjaZP5OZT02-gT9kQahbbCsltJb4SI).\
\
GEB is a modified fork of [MCD](https://github.com/makerdao/dss) that has several core differences:

* Variable names you [can actually understand](https://docs.tai.money/contract-translation/naming-transition)
* An autonomous feedback mechanism that changes the incentives of system participants
* The possibility to add insurance for SAFEs
* Fixed and increasing discount auctions (instead of English auctions) used to sell off collateral
* Automatic adjustment of several parameters in the system
* A set of contracts that bound control over parameters that are governed in the long run
* The possibility to send stability fees at once to multiple addresses
* The possibility to switch between surplus auctions and other types of strategies meant to remove surplus from the system
* Two prices for each `CollateralType`: one used for generating debt, the other one used exclusively when liquidating SAFEs
* A stability fee treasury that can pay for oracle calls or other contracts that automate the system
