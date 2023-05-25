---
description: Running a debt auction keeper in a Docker container
---

# Running in Docker

## 1. Get TAI

Buy TAI or [open a SAFE](https://app.gitbook.com/@money-god/s/geb/pyflex/safe-management/opening-a-safe) to generate it.

## 2. Modify the model file as needed

A basic debt auction bidding model can be found in `models/debt_model.py`. This model retrieves the latest RATE/USD price from Coingecko and will automatically place bids in an auction.

You probably want to modify the following variables in `models/debt_model.py`:

* `MAXIMUM_RATE_MULTIPLIER`: the maximum acceptable RATE price to use when bidding. Default: `0.90` meaning the maximum price to pay when biding for RATE (with TAI) is 90% of the current RATE/USD market price from Coingecko
* `MY_BID_DECREASE`: the bid decrease (in RATE) to propose when outbidding another bidder. If the value is smaller than the debt auction house's `bidDecrease`, then it will use the value set in the debt auction house. Example: a value of `1.10` will use bid decreases of 10%. Note: the current `bidDecrease` on mainnet is `1.03`

Then, use `chmod +x debt_model.py`.

For more information about bidding models, see [this](https://docs.tai.money/keepers/bidding-models).

## 3) Modify the keeper run file

Modify the following variables in `run_debt_keeper.sh`:

* `KEEPER_ADDRESS` - the keeper's address. It should be in checksummed format (not lowercase)
* `ETH_RPC_URL` - the URL of your Ethereum RPC connection
* `KEYSTORE_DIR` - the full path of the directory where your keystore file is
* `MODEL_DIR` - the full path of directory where your `surplus_model.py` file is
* `KEYSTORE_FILE` - your Ethereum UTC JSON keystore filename. For more information about the keystore format and how to generate it, check [Ethereum UTC / JSON Wallet Encryption](https://wizardforcel.gitbooks.io/practical-cryptography-for-developers-book/content/symmetric-key-ciphers/ethereum-wallet-encryption.html) or[ keythereum](https://github.com/ethereumjs/keythereum).
* `GAS_MAXIMUM` -maximum gas price, in GWEI

Then, use `chmod +x run_debt_keeper.sh`.

## 4) Start the keeper and enter your keystore file password

Use `./run_debt_keeper.sh`.

```
$ ./run_debt_keeper.sh
latest: Pulling from moneygod/auction-keeper
Digest: sha256:7e55ec9b0a136fc903d9f7f2690538bcbde9029d957e0e6f84d0282790f9666a
Status: Downloaded newer image for moneygod/auction-keeper:latest
docker.io/moneygod/auction-keeper:latest
Password for /keystore/key.json:
```

## Debt Auction Output

Sample[ debt auction output](running-in-docker.md#debt-auctioning-process)
