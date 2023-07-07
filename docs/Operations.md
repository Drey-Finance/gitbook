---
description: >-
  Drey is a decentralised actuarial operating system designed to deliver
  trustless bitcoin income streams for life.
---

# Actuary Operations

## Introduction

As previously described, Drey can be thought of as a collection of decentralised Drey Actuaries that achieve agreement and consensus and collectively take action on day to day operations that enable the achievement of its purpose: to deliver trustless bitcoin structured income streams that offer an alternative to third party intermediated annuities and pensions denominated in fiat.

To create a truly trustless bitcoin income plan, it is essential that Drey's actuarial models reflect the underpinnings that arise from operating in a decentralised manner from a technical perspective. The most critical point is the mechanics to ‘price’ participation and rewards in the fund, that they are easily understood if one were interrogating the embedded WASM binary or originating source code, while preserving a particular aspect called 'fairness,' inspired by the nominal-gain methodology.

Two methods of operation are novel in this respect.

First, Drey utilises Bitcoin[ ](https://www.galaxy.com/research/whitepapers/bitcoin-ordinals-inscriptions-5-billion-nft-market/)recursive inscriptions and zero knowledge proofs so that records are public, durable, verifiable and immutable. The operating system 'works out loud' for transparency and confidence. Identities are masked using zero-knowledge proof identity technology. Drey uses the Bitcoin blockchain itself to store data decentralised actuaries will come to a consensus on, such as actuarial tables in use and monthly distributions for the fund.

Second, Drey employs an accounting allocation method called **Dreybits**. The system allocates Dreybits to participants in the fund (customers), which is a method to price participation and schedule distributions in an aggressively transparent, decentralised manner which preserves fairness for all participants. **Dreybits are not DREY tokens**, they are a formalised accounting method that is designed to be an easily understood accounting convention designed to be relevant across lifetimes.

## Bitcoin Ordinals and Recursive Inscriptions

As written previously, Bitcoin's recursive inscriptions and ordinal theory have enabled bitcoin to be transformed into the world's most secure write once read only database.

All manner of Mime types can be inserted into a bitcoin blob space intrinsically linked to a specific satoshi, making the data both immutable and transferable. As Drey Finance will be keeping records that last lifespans, and in order to reduce shared object storage complexities that will no doubt arise if Drey Actuaries (miners) use a DHT or off chain storage, Drey uses bitcoin as the shared object storage, exploiting the ordinals system for the following use cases and more:

* Monthly investor distributions schedule per fund to be agreed upon by Drey Actuaries
* DAO proposals to be voted on by the Drey Actuaries
* Individual records pertaining to anonymous identity verification and authentication
* Individual records containing masked distribution information such as wallet address to send distributions
* Proof of Life confirmation records
* New or updated actuarial models to be deployed
* New or updated WASM binaries to be used in distribution calculations and accounting allocations

Two types of files will be stored in the Blockchain. WASM binaries and documents. Documents generated for insertion into bitcoin storage will use a defined schema and the [Apache Parquet file format ](https://parquet.apache.org/docs/overview/motivation/)compressed with [Briotli.](https://github.com/google/brotli) See the recommendations [here](https://www.lucidchart.com/techblog/2019/12/06/json-compression-alternative-binary-formats-and-compression-methods/).

The rest of this specification is described **in another technical section to be completed**.

## Drey Voting Protocol

Any Drey Actuary can create a DAO proposal by generating the a draft document within the Drey Actuary client which is broadcast to other members, seeking comment, inscribing the final draft at a particular satoshi, and relaying the satoshi ordinal value to other Drey Actuaries over the [Nostr protocol](https://nostr.com/) (built-in). The voting request announcement and document should contain a block height of when the vote will occur. A supermajority of Drey Actuaries will be required to vote through any proposal, distribution schedule or other material decision. Distribution schedules are assigned tasks as described below.

Each document in the Bitcoin blockchain will contain an address to forward the satoshi to that represents a yes or no. The same will also be described in the Nostr protocol vote request. The decentralised actuarial protocol embeds capability to create a transaction at x block height to move the satoshi to a specific wallet address denoting yes or no and declared in the Nostr communication and the document, indicating whether an issue or schedule was agreed to or not.&#x20;

This is accomplished by way of a Schnorr based threshold signature scheme, [ROAST](https://eprint.iacr.org/2022/550), using decentralized Nostr networks as a communication layer for a secure and encrypted method of transporting and digitally signing bitcoin transactions. This end-to-end solution solves issues with encrypted communication, coordination, optimization, and increased privacy for an enhanced threshold signature experience.

Each vote requires each Drey Actuaries to confirm their stance by engaging or ignoring the requested participation in the threshold signature scheme which results in a signed bitcoin transaction, moving the inscribed satoshi into a 'yes' wallet using funds which the Drey Actuaries control, creating a permanent records of vote confirmation.&#x20;

Using ROAST, Drey Actuaries have the ability to determine among themselves which Drey Actuaries voted for or against the proposal. However, to anyone observing the bitcoin blockchain, transactions generated by using the Schnorr threshold scheme enabled by the ROAST protocol look like any Pay-to-Taproot (P2TR) spend, thus preserving vote privacy outside of the Drey Actuary circle.\


## Dreybits

A Drey Actuary selected by verifiable random function, proposes a monthly distribution schedule called a Dreybit ledger based upon the WASM software packages each Drey Actuary runs to operate the fund. This proposed distribution schedule is written into the bitcoin blockchain at a specific satoshi and relayed to the Drey Actuary population over Nostr. The decentralised actuary system summons a vote by creating a transaction at _x_ block height to move the satoshi to a specific wallet address conveying acceptance or rejection.&#x20;

The Dreybit ledger contains each investor's allocated Dreybit amount to be received in each re-allocation cycle that occurs on the beginning of each month. Note that this is after an initial cycle at the initialisation of the fund at the beginning of month one. This process starts following the distribution of deceased member's Dreybits to survivors, and ultimately distribution of deceased member's bitcoin to surviving members which occurs at the end of the month.

Each Dreybit ledger contains an anonymized ID created for the user during signup which maps to their individual bitcoin allowance address and Dreybits allocated. The amount of Dreybits allocated depends on the investor’s probability of dying and amount invested (explained in a following section) relative to all investments in a particular fund.

The reason Dreybit ledgers must be re-updated monthly is to take into account variables such as the heuristics of the entire population at the beginning of the month since investors will move into new mortality rates as they age, previous investors pass away and are removed from the fund, new investors were added during the month, amounts invested as a pro-rata percentage of the entire value of the fund have changed, etc. These variables will change during the month, hence the allocated Dreybits to individual investor will change.

### Longevity Fund Terms and Conditions

Drey creates a set of binding off-chain smart contracts with terms and conditions which reflect the following stipulations that a longevity risk pooling fund naturally inherits:

* The investors in the fund agree that upon their deposit of bitcoin, this investment is an irrevocable gift to all other present and living participants in the fund who have already joined or will join in the future.
* This gift passes in entirety to the living participants in the fund when the contributing investor passes away
* It is held in escrow in a vault controlled by a super majority of Drey Actuaries&#x20;
* An investor’s allocation of their Dreybits is revoked/cancelled if-and-when the unit owners pass away
* He/she continues to enjoy the benefit of holding those Dreybits as long as they continuously (monthly) provide proof that he/she/they/them is/are alive within a certain time limit using the Drey Proof of Life app
* If such proof isn’t supplied, the rights conveyed by holding these Dreybits are forfeited, and ownership of the underlying bitcoin is distributed among those who did supply such proofs — i.e., proof of life. This is a type of [tontine agreement](https://en.wikipedia.org/wiki/Tontine).

### Other Mechanics

* Individuals can continuously invest in the fund and be assigned Dreybits at the beginning of the month
* Dreybits ARE NOT transferrable by action of the owner
* They are transferrable by action of the smart contracts only under control of the supermajority of Drey Actuaries
* Dreybits are calculated using satoshi as the base investment numbering system
* Yearly mortality rates are divisible by 12, to acclimate the rates to a monthly accounting.

## Dreybit Allocation Method

Dreybit allocation is specific to each individual user, so a scaling factor arises based on the the investor's probability of dying and their investment amount. For example, if an investor is 30 years old, a down scale occurs because their probability of living is much higher than a 65-year-old based on the actuarial data being used. This keeps the distributions fair via formulas inspired by the [nominal gain method](#user-content-fn-1)[^1].

Surviving members of a fair tontine do not receive equal allocations of each dying member’s forfeited balance.

Rather, they receive unequal allocations that depend on their respective mortality rate, _q_, and current account balance, _s_.

The intuition behind Dreybits and the allocation formulas are to maintain fairness on Dreybit distributions for everyone, regardless of your investment amount or life expectancy.

The allocation formula is as follows:

1. Determine the product of each individuals current balance in the fund in satoshi s with their mortality rate q. Acclimate a yearly mortality rate into a monthly rate by dividing the yearly rate by 12.
2. Determine the sum all products for each individual together.
3. Divide the sum by the total balance in the fund to get the weighted average.
4. The formula to determine the Dreybits allocated to an individual is the product of this weighted average and the individual's current balance.

$$p_{(1-ith)}= q_{(1-ith)} s_{(1-ith)}$$

$$\sum=p_{1}+p_{2}+p_{..ith}$$

$$\overline{W}=\frac{\sum}{s_(1-ith)}$$

$$DB_{(1-ith)}=\overline{W}s_{(1-ith)}$$

### Allocating Deceased's Distributions

When an existing investor passes away, Dreybits are re-allocated to the surviving investors. This step happens _BEFORE_ new investors are allocated Dreybits at the beginning of the month which results in a total re-allocation across the investor population. Note that even if no new investors were added, a re-allocation exercise is still necessary to take into account the removal of deceased members, changes in mortality rate, etc. The formula for determining the surviving members Dreybits received from the deceased members Dreybits is:

1. Sum the total of all deceased member's Dreybits in circulation at the end of the month.
2. Sum the total of all surviving member's Dreybits in circulation at the end of the month.
3. Determine a surviving individual's percentage of the sum of all deceased Dreybits allocated to all survivors by dividing their currently allocated Dreybits by the Sum all surviving member's Dreybits in circulation at the end of the month.
4. Multiply the individual's percentage by the Sum of all deceased member's Dreybits to determine Dreybits allocated.

$$\sum_{d}=DB_{(1-ith)} deceased$$

$$\sum_{s}=DB_{(1-ith)} surviving$$

$$x_{(1-ith)} =\frac{DB_{(1-i)}surviving}{\sum_{s}}$$

$$DB_{alloc(1-ith)}=\sum_{d}x_{(1-ith)}$$

The calculations are performed at the end of the month prior to new re-allocation exercise being performed.

These Dreybits are mapped to the sum of all the deceased's bitcoin by determining the pro-rata percentage allotment to be inherited of the total deceased's Dreybits for the period.

$$p_{(1-ith)} = \frac{DBalloc(1-ith)}{\sum_d}$$

$$\sum dec(btc) = sum\, of\, decased's\, bitcoin$$

$$p*\sum dec(btc) = percentage\, of\, \sum dec(btc)\, distributed$$

Note that this operation _MUST_ remove the deceased's Dreybits and hence the underlying bitcoin from the original fund and distribute the bitcoin to the survivors. However, the survivors have a choice of receiving this distribution directly to a wallet under their control, or, they can elect to deposit the received bitcoin (and monthly airdrop of DREY tokens) into a Drey savings/staking account, where the bitcoin and DREY tokens are deposited into a two-sided liquidity pool (DREY/BTC). This is explained in detail in the section on **Drey Savings accounts to be completed (TBC)**.

### Monthly Annuity Payment

In latest version of the system, rather than returning all of the deceased’s bitcoin every month to the survivors and emptying the sum of all deceased’s bitcoin out of the fund, the fund will redistribute the ownership of the bitcoin to surviving members but KEEP the bitcoin in the fund. A back of an envelope calculation sees that by doing so Drey greatly increase the bitcoin in the fund which drives an ever-increasing yield from the staking or lending operations. The individual investor will still experience an increase in their monthly distribution by way of the pro-rata assignment of deceased’s bitcoin to them which will also increase their ‘annuity like’ payment (from the remaining principal since their principal increases) and should increase their overall Dreybits allocation (unless perhaps there was a huge jump in new investors that month).

To determine the monthly payout, we use 120 as the age by which we expect all investors in the fund to live to for the USA, and for other locales we will use the last year by which mortality is expected to cease per that location's accepted mortality table. For the USA, we will use the 2012 IAM w/G2 scale for allocation operations.

$$1 + _{n}p_{x} / (1+i)^n + _{(n+1)}p_{x} / (1+i)^{(n+1) }+_{(n+2)}p_{x}$$

$$_{n}p_{x}$$ where _x_ is the current age of the annuitant, _n_ is the time from the current age until projected death (in months), and _p_ is the probability of survival to the next payment, and _i_ represents the discount rate.

As mentioned, for an annuity paid for life the formula continues until it is assumed the person cannot live longer (typically 120) but will rebalance based on new published and accepted mortality tables that enable the lifespan variable to increase.

### New Dreybit Monthly Re-Allocation

When a new investor joins and makes a deposit in any month, Dreybits are re-allocated to new and existing investors on the 1st of the month _AFTER_ deceased's Dreybits and bitcoin are allocated to existing investors and then removed from the fund _AND AFTER_ monthly annuity payments are remitted over the bitcoin network.

Therefore, a new weighted average is calculated using the new figures that naturally occur when removing the deceased members, paying monthly annuity payments, and optionally adding new investors (if there are any for the next month) into the fund.

$$p_{(1-ith)}= q_{(1-ith)} s_{(1-ith)}$$

$$\sum=p_{1}+p_{2}+p_{..ith}$$

$$\overline{W}=\frac{\sum}{s_(1-ith)}$$

The formula for new Dreybit monthly allocation per individual investor (new and existing) is as before, the product of their investment and the calculated weighted average.

$$DB_{(1-ith)}=\overline{W}s_{(1-ith)}$$

### Summarising Steps

1. At the initialisation of the fund, run the first Dreybit allocation step as described above.
2. Obtain a positive vote on the allocation schedule.
3. At the end of the month, tally the surviving member's share of deceased member's Dreybits.
4. Use this number to determine the pro-rata percentage of deceased member's bitcoin to be allocated to survivors.
5. Obtain a positive vote on the distribution schedule.
6. Remove the deceased member's Dreybits from the total and allocate the deceased member's bitcoin to survivor's balances.
7. Perform the APV of an Immediate Annuity formula to determine all fund investors' monthly payments.
8. Distribute the monthly payments to all fund investors via bitcoin network.
9. On the first of the month, re-run the Dreybit allocation steps and submit the re-allocation schedule for vote.
10. Obtain a positive vote on the re-allocation schedule.
11. Go to Step 3.

[^1]: Forman, J. B. and Sabin, M. J. (2016). Survivor funds. Pace Law Review, 37(1).
