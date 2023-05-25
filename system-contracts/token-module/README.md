---
description: >-
  ERC20 tokens, authority contracts and adapters for exiting and joining
  collateral in an out of the system
---

# Token Module

**Relevant smart contracts:**

* [DSDelegateToken](https://github.com/money-god/ds-token/blob/master/src/delegate.sol)
* [Coin](https://github.com/money-god/geb/blob/master/src/shared/Coin.sol)
* [BasicTokenAdapters](https://github.com/money-god/geb/blob/master/src/shared/BasicTokenAdapters.sol)
* [AdvancedTokenAdapters](https://github.com/money-god/geb-deploy/blob/master/src/AdvancedTokenAdapters.sol)
* [ProtocolTokenAuthority](https://github.com/money-god/geb-protocol-token-authority/blob/master/src/ProtocolTokenAuthority.sol)
* [GebPrintingPermissions](https://github.com/money-god/geb-printing-permissions/blob/master/src/GebPrintingPermissions.sol)

## 1. Overview <a id="1-introduction-summary"></a>

The token module has four distinct parts:

1. System Coin: token that the core system considers equal in value to its internal debt unit.
2. Protocol Token: a ds-token with delegation capabilities inherited from [UNI](https://uniswap.org/blog/uni/) which were in turn inherited from [COMP](https://compound.finance/governance/comp). It contains logic for burning and authorized minting. The token can be used to govern the system and as a recapitalization source.
3. Protocol Token Authority: authority contract that determines who is eligible to mint and burn protocol tokens.
4. Geb Printing Permissions: permissioning system to allow multiple debt auction contracts to mint protocol tokens.
5. Token Adapters:
   * Collateral Adapters: contracts that allow anyone to join or exit collateral in and out of GEB
   * Coin Join: adapter for the system coin to exit the system in the form of an ERC20 and enter the system in the form of `SAFEEngine.coinBalance`

## 2. Component Descriptions <a id="5-failure-modes-bounds-on-operating-conditions-and-external-risk-factors"></a>

* System Coin: this contract is the user facing ERC20 token maintaining the accounting for external system coin balances.
* Protocol Token: a token adhering to the ERC20 standard which also has [DSAuth](https://github.com/money-god/ds-auth)-protected mint and burn functions as well as delegation capabilities. The protocol token has two main use-cases:
  * **As a governance token:** tokens can be used as a representation of voting power
  * **As a recapitalization resource:** protocol tokens can autonomously be minted by the `DebtAuctionHouse` and sold for system coins which are used to recapitalize the system in times of insolvency
* Protocol Token Authority: determines who can mint and burn protocol tokens. Can be controlled directly by token holders, by the Protocol Token Authority or in some cases all control can be withdrawn from it.
* Geb Printing Permissions: forces governance to adhere to specific rules in order to allow multiple, independent `DebtAuctionHouse`s to print protocol tokens.
* Token Adapters: these are custom contracts that can allow anyone to deposit and withdraw collateral or they can have whitelisting in place to 

## 3. Risks <a id="5-failure-modes-bounds-on-operating-conditions-and-external-risk-factors"></a>

* The system coin is susceptible to the [ERC20 race condition](https://github.com/0xProject/0x-monorepo/issues/850)
* Emergency shutdown cannot be triggered if governance calls `PROTOCOL_TOKEN.stop` beforehand
* There is the possibility for a user to have their funds stolen by a malicious adapter which does not actually send tokens to the `SAFEEngine`, but instead to some other contract or wallet.

## 4. Governance Minimization

Governance can withdraw their voting power over all contracts, although, if they wish to allow the Protocol Token to protect multiple GEBs, they may retain influence over the Geb Printing Permissions.

All of the contracts in this module are part of Level 1 Gov Minimization.

