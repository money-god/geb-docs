# Geb Admin

This class extends the core `GEB` class with additional tools and contracts that are not used as often as other SAFE management tools. Here you will find utils for contracts such as DSPause, ESM etc. These contracts are scattered across several repositories. Please refer to the smart contract documentation to learn more about them.

**IMPORTANT:** To avoid bloating the main [geb.js](https://www.npmjs.com/package/geb.js) package this class is only available in a [separate package](https://www.npmjs.com/package/@money-god/geb-admin). Please install it like this:

```
npm install @money-god/geb-admin
```

And after that you are ready to use the admin tools similar to the GEB class:

```typescript
import { ethers } from 'ethers'
import { GebAdmin } from "@money-god/geb-admin"

 const provider = new ethers.providers.JsonRpcProvider('http://kovan.infura.io/<API KEY>')
 const gebAdmin = new GebAdmin('kovan', provider)
```

## Constructors

\+ **new GebAdmin**(`network`: GebDeployment, `provider`: GebProviderInterface | Provider): [_GebAdmin_](gebadmin.md)

_Defined in_ [_packages/geb-admin/src/geb-admin.ts:52_](https://github.com/money-god/geb.js/blob/30c41df/packages/geb-admin/src/geb-admin.ts#L52)

**Parameters:**

| Name       | Type                             | Description                                                                            |
| ---------- | -------------------------------- | -------------------------------------------------------------------------------------- |
| `network`  | GebDeployment                    | Either `'kovan'`, `'mainnet'` or an actual list of contract addresses.                 |
| `provider` | GebProviderInterface \| Provider | Either a Ethers.js provider or a GEB provider. Support for Web3.js will soon be added. |

**Returns:** [_GebAdmin_](gebadmin.md)

## Properties

### contracts

• **contracts**: _ContractApis_

_Inherited from_ [_GebAdmin_](gebadmin.md)_._[_contracts_](gebadmin.md#contracts)

Defined in packages/geb/lib/geb.d.ts:70

Object containing all GEB core smart-contracts instances for direct level interactions. All of the following contracts object are one-to-one typed API to the underlying smart-contract. Read-only functions that do not change the blockchain state return a promise of the return data. State modifying function will return synchronously a pre-filled transaction request object:

```
{
  to: "0x123abc.."
  data: "0xabab234ab..."
}
```

This object follow the [TransactionRequest model of ethers.js](https://docs.ethers.io/v5/api/providers/types/#providers-TransactionRequest) (Also similar to the [model used by web.js](https://web3js.readthedocs.io/en/v1.3.0/web3-eth.html#id84)). The object can be completed with properties such as `from`, `gasPrice`, `gas` (gas limit, web3.js ony) or `gasLimit` (gas limit, ethers.js only). The object can then be passed to the `sendTransaction` of [ehters.js](https://docs.ethers.io/v5/api/signer/#Signer-sendTransaction) or [web3.js](https://web3js.readthedocs.io/en/v1.3.0/web3-eth.html#sendtransaction)

Example:

```typescript
 // Setup geb.js an ethers
 const provider = new ethers.providers.JsonRpcProvider('http://kovan.infura.io/<API KEY>')
 const wallet = new ethers.Wallet('<Private key>', provider)
 const geb = new Geb('kovan', provider)

 // Contract read function: Fetch the debt ceiling
 const debtCeiling = await geb.contracts.safeEngine.globalDebtCeiling()

 // State changing function: Manualy liquidate a SAFE
 const tx = geb.contracts.liquidationEngine.liquidateSAFE(ETH_A, '0x1234abc...')
 await wallet.sendTransaction(tx) // Send the Ethereum transaction
```

Currently the following contracts ae available in this property:

* SAFEEngine
* AccountingEngine
* TaxCollector
* LiquidationEngine
* OracleRelayer
* GlobalSettlement
* DebtAuctionHouse
* PreSettlementSurplusAuctionHouse
* PostSettlementSurplusAuctionHouse
* SettlementSurplusAuctioneer
* GebSafeManager
* GetSafes
* BasicCollateralJoin
* CoinJoin
* Coin (System coin ERC20 contract)
* GebProxyRegistry
* FixedDiscountCollateralAuctionHouse
* Weth (ERC20)

For detailed information about the functions of each contract we recommend referring directly to the smart-contract [code](https://github.com/money-god/geb) and [documentation](https://docs.tai.money/)

### contractsAdmin

• **contractsAdmin**: _AdminApis_

_Defined in_ [_packages/geb-admin/src/geb-admin.ts:52_](https://github.com/money-god/geb.js/blob/30c41df/packages/geb-admin/src/geb-admin.ts#L52)

Object containing all GEB admin contracts instances for low level interactions. It currently has the following contracts:

* MultiSigWallet
* DsProxy
* DsToken
* ProtocolTokenAuthority
* GebPollingEmitter
* GebPrintingPermissions
* DsDelegateRoles
* DsPause
* DsPauseProxy
* GovActions
* ESM
* TokenBurner
* FsmGovernanceInterface
* DsProxyFactory
* GebDeployPauseProxyActions
* DsProxy
* TxManager

## Methods

### deployProxy

▸ **deployProxy**(): _object_

_Inherited from_ [_GebAdmin_](gebadmin.md)_._[_deployProxy_](gebadmin.md#deployproxy)

Defined in packages/geb/lib/geb.d.ts:88

Deploy a new proxy owned by the sender.

**Returns:** _object_

* **chainId**? : _number_
* **data**? : _string_
* **from**? : _string_
* **gasLimit**? : _BigNumber_
* **gasPrice**? : _BigNumber_
* **nonce**? : _number_
* **to**? : _string_
* **value**? : _BigNumber_

### getErc20Contract

▸ **getErc20Contract**(`tokenAddress`: string): _Erc20_

_Inherited from_ [_GebAdmin_](gebadmin.md)_._[_getErc20Contract_](gebadmin.md#geterc20contract)

Defined in packages/geb/lib/geb.d.ts:123

Returns an object that can be used to interact with a ERC20 token. Example:

```typescript
const USDCAddress = "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48"
const USDC = geb.getErc20Contract(USDCAddress)

// Get 0xdefiisawesome's balance
const balance = USDC.balanceOf("0xdefiisawesome..")

// Send 1 USDC to 0xdefiisawesome (USDC is 6 decimals)
const tx = USDC.transfer("0xdefiisawesome..", "1000000")
await wallet.sendTransaction(tx)
```

**Parameters:**

| Name           | Type   | Description            |
| -------------- | ------ | ---------------------- |
| `tokenAddress` | string | Token contract address |

**Returns:** _Erc20_

Erc20

### getGebContract

▸ **getGebContract**‹**T**›(`gebContractClass`: GebContractAPIConstructorInterface‹T›, `address`: string): _T_

_Inherited from_ [_GebAdmin_](gebadmin.md)_._[_getGebContract_](gebadmin.md#static-getgebcontract)

Defined in packages/geb/lib/geb.d.ts:165

Returns an instance of a specific geb contract given a Geb contract API class at a specified address

```typescript
import { contracts } from "geb.js"
const safeEngine = geb.getGebContract(contracts.SafeEngine, "0xabcd123..")
const globalDebt = safeEngine.globalDebt()
```

**Type parameters:**

▪ **T**: _BaseContractAPI_

**Parameters:**

| Name               | Type                                  | Description                            |
| ------------------ | ------------------------------------- | -------------------------------------- |
| `gebContractClass` | GebContractAPIConstructorInterface‹T› | Class from contracts or adminContracts |
| `address`          | string                                | Contract address of the instance       |

**Returns:** _T_

### getIncentiveCampaignContract

▸ **getIncentiveCampaignContract**(`campaignNumber`: number): _Promise‹StakingRewards›_

_Inherited from_ [_GebAdmin_](gebadmin.md)_._[_getIncentiveCampaignContract_](gebadmin.md#getincentivecampaigncontract)

Defined in packages/geb/lib/geb.d.ts:131

Help function to get the contract object of an incentive campaign given its number ID

**Parameters:**

| Name             | Type   | Description                    |
| ---------------- | ------ | ------------------------------ |
| `campaignNumber` | number | incremental ID of the campaign |

**Returns:** _Promise‹StakingRewards›_

StakingRewards

### getProxyAction

▸ **getProxyAction**(`ownerAddress`: string): _Promise‹GebProxyActions›_

_Inherited from_ [_GebAdmin_](gebadmin.md)_._[_getProxyAction_](gebadmin.md#getproxyaction)

Defined in packages/geb/lib/geb.d.ts:84

Given an address returns a GebProxyActions object to execute bundled operations. Important: This requires the address to have deployed a GEB proxy through the proxy registry contract. It will throw a `DOES_NOT_OWN_HAVE_PROXY` error if the address specified does not have a proxy. Use the [deployProxy](gebadmin.md#deployproxy) function to get a new proxy.

**Parameters:**

| Name           | Type   | Description                                                            |
| -------------- | ------ | ---------------------------------------------------------------------- |
| `ownerAddress` | string | Externally owned user account, Ethereum address that owns a GEB proxy. |

**Returns:** _Promise‹GebProxyActions›_

### getSafe

▸ **getSafe**(`idOrHandler`: string | number, `collateralType?`: string): _Promise‹Safe›_

_Inherited from_ [_GebAdmin_](gebadmin.md)_._[_getSafe_](gebadmin.md#getsafe)

Defined in packages/geb/lib/geb.d.ts:93

Get the SAFE object given a `safeManager` id or a `safeEngine` handler address.

**Parameters:**

| Name              | Type             | Description             |
| ----------------- | ---------------- | ----------------------- |
| `idOrHandler`     | string \| number | Safe Id or SAFE handler |
| `collateralType?` | string           | -                       |

**Returns:** _Promise‹Safe›_

### getSafeFromOwner

▸ **getSafeFromOwner**(`address`: string): _Promise‹Safe\[]›_

_Inherited from_ [_GebAdmin_](gebadmin.md)_._[_getSafeFromOwner_](gebadmin.md#getsafefromowner)

Defined in packages/geb/lib/geb.d.ts:104

Fetch the list of safes owned by an address. This function will fetch safes owned directly through the safeManager and safes owned through the safe manager through a proxy. Safes owned directly by the address at the safeEngine level won't appear here.

Note that this function will make a lot of network calls and is therefore very slow. For front-ends we recommend using pre-indexed data such as the geb-subgraph.

**Parameters:**

| Name      | Type   | Description |
| --------- | ------ | ----------- |
| `address` | string |             |

**Returns:** _Promise‹Safe\[]›_

### gnosisSafeThreshold1SubmitTransaction

▸ **gnosisSafeThreshold1SubmitTransaction**(`sender`: string, `to`: string, `data`: string): _TransactionRequest_

_Defined in_ [_packages/geb-admin/src/geb-admin.ts:203_](https://github.com/money-god/geb.js/blob/30c41df/packages/geb-admin/src/geb-admin.ts#L203)

Submit a transaction to a gnosis safe directly executed. Works only if the threshold on the safe is 1.

**Parameters:**

| Name     | Type   | Description                        |
| -------- | ------ | ---------------------------------- |
| `sender` | string | Proposal submitter                 |
| `to`     | string | Proposal target (Usually ds-pause) |
| `data`   | string | transaction data of the proposal   |

**Returns:** _TransactionRequest_

### multiCall

▸ **multiCall**‹**O1**, **O2**, **O3**›(`calls`: \[MulticallRequest‹O1›, MulticallRequest‹O2›, MulticallRequest‹O3›]): _Promise‹\[O1, O2, O3]›_

_Inherited from_ [_GebAdmin_](gebadmin.md)_._[_multiCall_](gebadmin.md#multicall)

Defined in packages/geb/lib/geb.d.ts:136

**Type parameters:**

▪ **O1**

▪ **O2**

▪ **O3**

**Parameters:**

| Name    | Type                                                                |
| ------- | ------------------------------------------------------------------- |
| `calls` | \[MulticallRequest‹O1›, MulticallRequest‹O2›, MulticallRequest‹O3›] |

**Returns:** _Promise‹\[O1, O2, O3]›_

### verifyWebScheduleCallcode

▸ **verifyWebScheduleCallcode**(`govFunctionAbi`: string, `params`: any\[], `earliestExecutionTime`: number, `calldata`: string, `description?`: string): _Promise‹boolean›_

_Defined in_ [_packages/geb-admin/src/geb-admin.ts:75_](https://github.com/money-god/geb.js/blob/30c41df/packages/geb-admin/src/geb-admin.ts#L75)

Verifies a transaction for scheduling proposals

**Parameters:**

| Name                    | Type   | Description                                                                           |
| ----------------------- | ------ | ------------------------------------------------------------------------------------- |
| `govFunctionAbi`        | string | Human readable abi from gov actions or proxy of choice -> "setDelay(address,uint256)" |
| `params`                | any\[] | Array containing all for the above function                                           |
| `earliestExecutionTime` | number | -                                                                                     |
| `calldata`              | string | to verify                                                                             |
| `description?`          | string | -                                                                                     |

**Returns:** _Promise‹boolean›_

Promise

### webExecuteProposal

▸ **webExecuteProposal**(`govFunctionAbi`: string, `params`: any\[], `earliestExecutionTime`: number): _Promise‹TransactionRequest›_

_Defined in_ [_packages/geb-admin/src/geb-admin.ts:99_](https://github.com/money-god/geb.js/blob/30c41df/packages/geb-admin/src/geb-admin.ts#L99)

Encodes executing a proposal in dspause for web GUI

**Parameters:**

| Name                    | Type   | Description                                                                           |
| ----------------------- | ------ | ------------------------------------------------------------------------------------- |
| `govFunctionAbi`        | string | Human readable abi from gov actions or proxy of choice -> "setDelay(address,uint256)" |
| `params`                | any\[] | Array containing all for the above function                                           |
| `earliestExecutionTime` | number | -                                                                                     |

**Returns:** _Promise‹TransactionRequest›_

Promise

### webScheduleProposal

▸ **webScheduleProposal**(`govFunctionAbi`: string, `params`: any\[], `earliestExecutionTime`: number, `description?`: string): _Promise‹object›_

_Defined in_ [_packages/geb-admin/src/geb-admin.ts:124_](https://github.com/money-god/geb.js/blob/30c41df/packages/geb-admin/src/geb-admin.ts#L124)

Encodes scheduling a proposal in dspause for web GUI

**Parameters:**

| Name                    | Type   | Description                                                                           |
| ----------------------- | ------ | ------------------------------------------------------------------------------------- |
| `govFunctionAbi`        | string | Human readable abi from gov actions or proxy of choice -> "setDelay(address,uint256)" |
| `params`                | any\[] | Array containing all for the above function                                           |
| `earliestExecutionTime` | number | -                                                                                     |
| `description?`          | string | -                                                                                     |

**Returns:** _Promise‹object›_

Promise

### webTestScheduleProposal

▸ **webTestScheduleProposal**(`govFunctionAbi`: string, `params`: any\[], `earliestExecutionTime`: number, `description?`: string): _Promise‹void›_

_Defined in_ [_packages/geb-admin/src/geb-admin.ts:173_](https://github.com/money-god/geb.js/blob/30c41df/packages/geb-admin/src/geb-admin.ts#L173)

Test the execution of a proposal about to be schedule in dspause with web GUI

**Parameters:**

| Name                    | Type   | Description                                                                           |
| ----------------------- | ------ | ------------------------------------------------------------------------------------- |
| `govFunctionAbi`        | string | Human readable abi from gov actions or proxy of choice -> "setDelay(address,uint256)" |
| `params`                | any\[] | Array containing all for the above function                                           |
| `earliestExecutionTime` | number | -                                                                                     |
| `description?`          | string | -                                                                                     |

**Returns:** _Promise‹void›_

Promise

### `Static` getGebContract

▸ **getGebContract**‹**T**›(`gebContractClass`: GebContractAPIConstructorInterface‹T›, `address`: string, `provider`: GebProviderInterface | Provider): _T_

_Inherited from_ [_GebAdmin_](gebadmin.md)_._[_getGebContract_](gebadmin.md#static-getgebcontract)

Defined in packages/geb/lib/geb.d.ts:152

Returns an instance of a specific geb contract given Geb contract API class constructor at a specified address

**Type parameters:**

▪ **T**: _BaseContractAPI_

**Parameters:**

| Name               | Type                                  | Description                                   |
| ------------------ | ------------------------------------- | --------------------------------------------- |
| `gebContractClass` | GebContractAPIConstructorInterface‹T› | Class from contracts or adminContracts        |
| `address`          | string                                | Contract address of the instance              |
| `provider`         | GebProviderInterface \| Provider      | Either a Ethers.js provider or a Geb provider |

**Returns:** _T_
