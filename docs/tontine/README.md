---
description: Draft 2.0
---

# Fair Tontine Calculations/Operations

## How Drey Works

To create a truly trustless bitcoin income plan, it is essential that our models reflect the actual way that Drey works from a technical perspective, and the way we ‘price’ participation in the fund is easily understood while preserving fairness using a nominal-gain methodology. We will also be utilising [bitcoin inscription/ordinals](https://www.galaxy.com/research/whitepapers/bitcoin-ordinals-inscriptions-5-billion-nft-market/), so that records are public, (identities are masked), durable and immutable. In other words, we will be using the bitcoin blockchain itself to store data decentralised actuaries will come to a consensus on, such as monthly distributions for the fund.

### Bitcoin Ordinals and Inscriptions

Bitcoin inscriptions and ordinal theory have enabled bitcoin to be transformed into the world's most secure write once read only database.&#x20;

All manner of Mime types can be inserted into a bitcoin blob space intrinsically linked to a specific satoshi, making the data both immutable and transferable. Because Drey Finance will be keeping records that last lifespans, and in order to reduce shared object storage complexities that will no doubt arise if miners use a DHT, Drey will instead use bitcoin as the shared object storage, exploiting the ordinals system for the following use cases:

* Monthly investor distributions schedule per fund to be agreed upon by the miners
* DAO proposals to be voted on by the miners
* Individual records pertaining to anonymous identity verification and authentication
* Individual records containing distribution information such as wallet address to send distributions
* Individual records containing general account information
* Proof of Life confirmation records
* New or updated actuarial models to be deployed
* New or updated R software models to be used in distribution calculations (TBD)

Documents generated for insertion into bitcoin storage will use a defined schema (TBC) on [JSON-LD documents](https://en.wikipedia.org/wiki/JSON-LD) compressed with [Briotli.](https://github.com/google/brotli) See the recommendations [here](https://www.lucidchart.com/techblog/2019/12/06/json-compression-alternative-binary-formats-and-compression-methods/).

The rest of this specification and will be broken out into its own section to be completed.

### Voting

Any Drey miner can call for a vote on any proposed distribution schedule or DAO proposal by generating the document, inscribing it at a particular satoshi, and relaying the satoshi ordinal value to any other miner over the [nostr protocol](https://nostr.com/). The voting request announcement and JSON-LD document should contain a block height of when the vote will occur. A supermajority of miners will be required to vote any proposal, distribution schedule or other material decision through.&#x20;

Each JSON-LD document in the Bitcoin blockchain will contain an address to forward the satoshi to that represents a yes or no. The same will also be described in the nostr protocol vote request. The decentralised miner protocol will be used to create a transaction at x block height to move the satoshi to a specific wallet address denoting yes or no and declared in the nostr communication and the JSON-LD document, indicating whether an issue or schedule was agreed to or not.

### Dreybits

A Drey miner, selected by verifiable random function, proposes a monthly distribution schedule called a Dreybit ledger based upon the R software packages each miner runs to operate the fund. This proposed distribution schedule is written into the bitcoin blockchain at a specific satoshi and relayed to the miner population over nostr. The decentralised miner protocol will be asked to create a transaction at x block height to move the satoshi to a specific wallet address conveying acceptance or rejection.

The Dreybit ledger contains each investors allocated bitcoin amounts to be received in the next distribution. Each Dreybit ledger alias ID is created for the user during signup which maps to their bitcoin address and amount of bitcoin to be received. The amount of bitcoin an investor gets depends on the investor’s probability of dying and amount invested (explained in a following section) relative to all investment in the fund.

At the end of every month, a new Dreybit ledger is created with updated Dreybits allocated to all investors. Ledgers must be updated to take into account variables such as the heuristics of the entire population at the beginning of the month since investors will move into new mortality rates as they age, new investors were added during the month, amount invested as a pro-rata percentage of the entire value of the fund, etc.

An investor’s allocation of their Dreybits is revoked/cancelled if-and-when the assignees pass away. He/she continues to enjoy the benefit of holding those Dreybits month to month as long as they continuously (monthly) provide proof that you he/she is alive within a certain time limit.

If such proof isn’t supplied, the rights conveyed by holding these Dreybits are forfeited, and ownership of the underlying bitcoin is distributed among those who did supply such proofs—that is they are still alive. This is a type of tontine agreement.

## Fair Tontine Tontine Forfeiture Allocation

Surviving members of a fair tontine do not receive equal allocations of each dying member’s forfeited balance.

Rather, they receive unequal allocations that depend on their respective mortality rate, _q_, and account balance, _s_.

One useful property of this method is that it promotes transparency by being easily decomposed into two simple components: (1) a nominal tontine (life credit) yield for each member, which is easily obtained from the tontine’s mortality table, and, (2) a common adjustment factor that accounts for the difference between the amount of forfeitures experienced by the pool during a given period and the amount that was nominally expected, plus the amount expected from the investment yield.

A “nominal-gain method” described in Sabin and Forman (2016), which is desirable for its relative simplicity and explanatory properties enables the realisation of fair tontine forfeiture.

### Terms and Conditions

Drey creates a set of binding smart contracts and terms and conditions which reflect the following stipulations:

* The investors in the fund agree that upon their deposit of bitcoin, this investment is an irrevocable gift to all other present and living participants in the fund who have already joined or will join in the future.
* This gift passes in entirety to the living participants in the fund when the contributing investor passes away.
* It is held in escrow in a smart contract until then, with the smart contract issuing monthly payments based on a fraction of principal calculated using the maximum life date based on actuarial data.
* An investor’s allocation of their Dreybits is revoked/cancelled if-and-when the unit owners pass away.&#x20;
* He/she continues to enjoy the benefit of holding those Dreybits as long as they continuously (monthly) provide proof that you he/she is alive within a certain time limit.&#x20;
* If such proof isn’t supplied, the rights conveyed by holding these Dreybits are forfeited, and ownership of the underlying bitcoin is distributed among those who did supply such proofs—that is they are still alive. This is a type of [tontine agreement](https://en.wikipedia.org/wiki/Tontine).

### Other Mechanics

* Dreybits can be issued at any time, so people can continuously invest in the tontine and be assigned Dreybits.&#x20;
* Dreybits ARE NOT transferrable by action of the owner.&#x20;
* They are transferrable by action of the smart contracts only.
* Dreybits are calculated using satoshi as units, not btc.

Dreybit pricing is specific to each individual user, so the base price is modified based on the the investors probability of dying and their investment amount. For example, if an investor is 30 years old, a step-up in price to acquire Dreybits occurs because their probability of living is much higher than a 65-year-old based on the actuarial data. This keeps the distributions fair via the nominal gain method.

SECTION FROM CFA PAPER HERE.

## Dreybit Pricing

The intuition behind the pricing scheme is to maintain the fairness of the tontine and properly price Dreybits for everyone using the nominal tontine yield formula mentioned earlier $$(r = q / (1 - q))$$ and apply it to calculate the required step-up or discount off the base rate for each investor.

To achieve fairness and accurate pricing, we first determine a weighted average on the product of mortality risk and investment in the fund by:

1. Determine the product of each individuals current balance in the fund in satoshi $$s$$with their mortality rate $$q$$ and sum all individuals in the fund together. &#x20;
2. Divide the sum by the total balance in the fund to get the weighted average.
3. The formula to determine the Dreybit price for an individual is the product of this weighted average and their investment amount.



### New Dreybit Monthly Allocation

When a new investor joins, Dreybits are allocated to the investor on the 1st of the month following their deposit.&#x20;

Dreybits are not reallocated to existing investors, simply, new Dreybits are allocated new investors.

The formula for new Dreybit monthly allocation per individual investor is as before, the product of their investment and the calculated weighted average.

These additional Dreybits change the overall amount of Dreybits in circulation but do not change the amount of Dreybits already allocated to individuals.

### Allocating Deceased Distributions

When an existing investor passes away, Dreybits are re-allocated to the surviving investors. The formula for determining the surviving members Dreybits received from the deceased members Dreybits is:

1. Sum the total of all deceased member's Dreybits in circulation at the end of the month.
2. Create the product of the Sum and an individual's Dreybits.
3. Divide by the sum of the total of all surviving member's Dreybits in circulation at the end of the month.

The calculations are performed at the end of the month. These Dreybits will be converted into bitcoin and distributed to the surviving members at the beginning of each month, removing them from the monthly re-allocation process.

### New Dreybit Monthly Re-Allocation

At the beginning of the month, after the deceased Dreybits are distributed to survivors, a new weighted average is calculated using the new figures that naturally occur when removing the deceased members.
