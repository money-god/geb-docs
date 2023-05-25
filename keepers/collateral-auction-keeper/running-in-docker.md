---
description: Running a collateral auction-keeper in a docker container.
---

# Running in Docker

## 1\) Get TAI

Buy TAI from Uniswap v2 or [open a SAFE](https://app.gitbook.com/@money-god/s/geb/pyflex/safe-management/opening-a-safe) and generate it.

## 2\) Create the keeper run file

Create a file called `run_auction_keeper.sh` and paste the following code in it:

```text
#!/bin/bash

docker run -it \
    -v <KEYSTORE DIR>:/keystore \
    moneygod/auction-keeper:latest \
        --rpc-uri <ETH_RPC_URL> \
        --eth-from <KEEPER ADDRESS> \
        --eth-key key_file=/keystore/<KEYSTORE FILE>
```

### Then, substitute the following variables:

`KEYSTORE_DIR` - the local directory where your keystore file is

`KEYSTORE_FILE` - your Ethereum UTC JSON keystore filename

For more information about this keystore format and how to generate them:

* [Ethereum UTC / JSON Wallet Encryption](https://wizardforcel.gitbooks.io/practical-cryptography-for-developers-book/content/symmetric-key-ciphers/ethereum-wallet-encryption.html)
* [keythereum](https://github.com/ethereumjs/keythereum)

`ETH_RPC_URL` - the URL of the ethereum RPC connection

`KEEPER_ADDRESS` - the keeper's address. It must be in a checksummed format

### Finally:

`chmod +x run_auction_keeper.sh`

## 3\) Start the keeper and enter your keystore file password

`./run_auction_keeper.sh`

```text
$ ./run_auction_keeper.sh
latest: Pulling from moneygod/auction-keeper
Digest: sha256:7e55ec9b0a136fc903d9f7f2690538bcbde9029d957e0e6f84d0282790f9666a
Status: Downloaded newer image for moneygod/auction-keeper:latest
docker.io/moneygod/auction-keeper:latest
Password for /keystore/key.json:
```

