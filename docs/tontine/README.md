---
description: Draft 2.0
---

# Fair Tontine Calculations/Operations

## How Drey Works

To create a truly trustless bitcoin income plan, it is essential that our models reflect the actual way that Drey works from a technical perspective, and the way we ‘price’ participation in the fund is easily understood while preserving fairness inspired by the nominal-gain methodology in Sabin and Forman (2016).&#x20;

Drey utilises [bitcoin inscription/ordinals](https://www.galaxy.com/research/whitepapers/bitcoin-ordinals-inscriptions-5-billion-nft-market/), so that records are public, (identities are masked), durable and immutable. In other words, Drey uses the bitcoin blockchain itself to store data decentralised actuaries will come to a consensus on, such as monthly distributions for the fund.

### Bitcoin Ordinals and Inscriptions

Bitcoin inscriptions and ordinal theory have enabled bitcoin to be transformed into the world's most secure write once read only database.&#x20;

All manner of Mime types can be inserted into a bitcoin blob space intrinsically linked to a specific satoshi, making the data both immutable and transferable. Because Drey Finance will be keeping records that last lifespans, and in order to reduce shared object storage complexities that will no doubt arise if miners use a DHT or off chain storage, Drey uses bitcoin as the shared object storage, exploiting the ordinals system for the following use cases:

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

Any Drey miner can call for a vote on any proposed distribution schedule or DAO proposal by generating the document, inscribing it at a particular satoshi, and relaying the satoshi ordinal value to any other miner over the [nostr protocol](https://nostr.com/). The voting request announcement and JSON-LD document should contain a block height of when the vote will occur. A supermajority of miners will be required to vote through any proposal, distribution schedule or other material decision.&#x20;

Each JSON-LD document in the Bitcoin blockchain will contain an address to forward the satoshi to that represents a yes or no. The same will also be described in the nostr protocol vote request. The decentralised miner protocol will be used to create a transaction at x block height to move the satoshi to a specific wallet address denoting yes or no and declared in the nostr communication and the JSON-LD document, indicating whether an issue or schedule was agreed to or not.

## Dreybits

A Drey miner, selected by verifiable random function, proposes a monthly distribution schedule called a Dreybit ledger based upon the R software packages each miner runs to operate the fund. This proposed distribution schedule is written into the bitcoin blockchain at a specific satoshi and relayed to the miner population over nostr. The decentralised miner protocol will be asked to create a transaction at x block height to move the satoshi to a specific wallet address conveying acceptance or rejection.

The Dreybit ledger contains each investors allocated Dreybits amounts to be received in each re-allocation cycle that occurs on the beginning of each month (an initial cycle at the initialisation of the fun). Each Dreybit ledger contains an alias ID created for the user during signup which maps to their bitcoin address and Dreybits allocated. The amount of Dreybits allocated depends on the investor’s probability of dying and amount invested (explained in a following section) relative to all investment in the fund.

At the beginning of every month, a new proposed Dreybit ledger is created with updated Dreybits re-allocated to all surviving investors. Ledgers must be re-updated monthly to take into account variables such as the heuristics of the entire population at the beginning of the month since investors will move into new mortality rates as they age, new investors were added during the month, previous investors pass away, amounts invested as a pro-rata percentage of the entire value of the fund have changed, etc.

### Fair Tontine Tontine Forfeiture Allocation

Surviving members of a fair tontine do not receive equal allocations of each dying member’s forfeited balance.

Rather, they receive unequal allocations that depend on their respective mortality rate, _q_, and current account balance, _s_.

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

* Individuals can continuously invest in the fund and be assigned Dreybits at the beginning of the month.&#x20;
* Dreybits ARE NOT transferrable by action of the owner.&#x20;
* They are transferrable by action of the smart contracts only.
* Dreybits are calculated using satoshi as units, not btc.

Dreybit allocation is specific to each individual user, so a scaling factor arises based on the the investors probability of dying and their investment amount. For example, if an investor is 30 years old, a down scale occurs because their probability of living is much higher than a 65-year-old based on the actuarial data. This keeps the distributions fair via the nominal gain method.

SECTION FROM CFA PAPER HERE.

## Dreybit Allocation Method

The intuition behind the pricing scheme is to maintain the fairness of the tontine and properly allocated Dreybits for everyone using the nominal tontine yield formula mentioned earlier $$(r = q / (1 - q))$$ and apply it to calculate the required step-up or discount off the base rate for each investor.

The allocation formula is as follows:

1. Determine the product of each individuals current balance in the fund in satoshi s with their mortality rate q.
2. Determine the sum all products for each individual together. &#x20;
3. Divide the sum by the total balance in the fund to get the weighted average.
4. The formula to determine the Dreybits allocated to an individual is the product of this weighted average and the individual's current balance.

$$p_{(1-ith)}= q_{(1-ith)} s_{(1-ith)}$$

$$\sum=p_{1}+p_{2}+p_{..ith}$$

$$\overline{W}=\frac{\sum}{s_(1-ith)}$$

$$DB_{(1-ith)}=\overline{W}s_{(1-ith)}$$

### Allocating Deceased's Distributions

When an existing investor passes away, Dreybits are re-allocated to the surviving investors. This step happens _BEFORE_ new investors are allocated Dreybits at the beginning of the month which results in a total re-allocation across the investor population. The formula for determining the surviving members Dreybits received from the deceased members Dreybits is:

1. Sum the total of all deceased member's Dreybits in circulation at the end of the month.
2. Sum the total of all surviving member's Dreybits in circulation at the end of the month.
3. Determine a surviving individual's percentage of the sum of all deceased Dreybits allocated to all survivors by dividing their currently allocated Dreybits by the Sum all surviving member's Dreybits in circulation at the end of the month.
4. Multiply the individual's percentage by the Sum of all deceased member's Dreybits to determine Dreybits allocated.

$$\sum_{d}=DB_{(1-ith)} deceased$$

$$\sum_{s}=DB_{(1-ith)} surviving$$

$$x_{(1-ith)} =\frac{DB_{(1-i)}surviving}{\sum_{s}}$$

$$DB_{new(1-ith)}=\sum_{d}x_{(1-ith)}$$

The calculations are performed at the end of the month prior to new investors being allocated new Dreybits.&#x20;

These Dreybits are mapped to the sum of all the deceased's bitcoin by determining the pro-rata percentage allotment to be inherited of the total deceased's Dreybits for the period.

$$p_{(1-ith)} = \frac{DBnew(1-ith)}{\sum_d}$$

$$\sum dec(btc) = sum\, of\, decased's\, bitcoin$$

$$p*\sum dec(btc) = percentage\, of\, \sum dec(btc)\, distributed$$

### New Dreybit Monthly Re-Allocation

When a new investor joins and makes a deposit in any month, Dreybits are re-allocated to new and existing investors on the 1st of the month following _AFTER_ deceased's Dreybits and bitcoin are allocated to existing investors and then removed from the fund.&#x20;

Therefor, a new weighted average is calculated using the new figures that naturally occur when removing the deceased members.

$$p_{(1-ith)}= q_{(1-ith)} s_{(1-ith)}$$

$$\sum=p_{1}+p_{2}+p_{..ith}$$

$$\overline{W}=\frac{\sum}{s_(1-ith)}$$

The formula for new Dreybit monthly allocation per individual investor (new and existing) is as before, the product of their investment and the calculated weighted average.

$$DB_{(1-ith)}=\overline{W}s_{(1-ith)}$$

### Summarising Steps

1. At the initialisation of the fund, run the first Dreybit allocation step as described above.
2. At the end of the month, tally the surviving member's share of deceased member's Dreybits.
3. Use this number to determine the pro-rata percentage of deceased member's bitcoin to be allocated to survivors.
4. Remove the deceased member's Dreybits from the total and remit the deceased member's bitcoin to survivors.
5. On the first of the month, re-run the Dreybit allocation steps.
