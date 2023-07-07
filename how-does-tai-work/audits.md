# Audits

TAI is a fork of Reflexer's RAI, which has been audited by [OpenZeppelin](https://github.com/reflexer-labs/geb-audits/tree/master/open-zeppelin/core-contracts) and [Quantstamp](https://github.com/reflexer-labs/geb-audits/tree/master/quantstamp/helper-contracts). Anyone can verify TAI is a fork of RAI, as all [TAI contracts ](../tai-protocol-in-depth/contracts/contract-addresses.md)are verified on Etherscan.

The changes made to the RAI code are _**extremely minimal**_, as RAI already had multi-collateral support.

#### Core Code Changes from RAI

1\) Add debt rewards

&#x20;Keep track of when debt is minted or repaid in the Safe Engine so debt rewards can be paid.

2\) Collateral auction improvements

Decrease minimum discount collateral can be sold for at auction, improving user experience of liquidated safes.

Remove caching of the redemption price in the collateral auction contract.









