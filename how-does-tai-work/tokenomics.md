# Tokenomics

## RATE Allocation

Total RATE Supply: 1,000,000

Team: 10%

Treasury: 7%

Community Rewards: 78%

Community Treasury: 5%

## Buyback and Burn

TAI uses the 'buyback and burn' strategy of DAI/RAI.

Fees from TAI loans produce revenue for the system. This revenue is in the form of TAI and is initially used to seed a small `surplus buffer` of TAI. Revenue is also used to pay for system calls that update collateral prices, collect fees, and maintain the protocol.&#x20;

TAI that is remaining after these expenses is deemed `surplus` and is auctioned in exchange for RATE. The collected RATE is then burned and the supply is deflated, hence the name 'buyback and burn'.

## Mint and Sell

\
The above 'buyback and burn' scenario is what happens during normal operation of the protocol. This 'mint and sell' safety mechanism ensures the system can function in extreme market conditions. &#x20;

During very large collateral price drops(or oracle failures) it is possible a safe for a safe to have more debt than the value of collateral locked. In this scenario, the system will use TAI from the `surplus buffer` to cover the excess debt the safe has. If the surplus buffer has already been exhausted from covering other underwater safes, the system has incurred `bad debt`.

To cover the bad debt the system will mint RATE, inflating the supply, and then sell it for TAI. The TAI is then used to cover the bad debt.



