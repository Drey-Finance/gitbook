---
description: >-
  Draft 3.0 describes a system where bitcoin from deceased is layered into a
  monthly annuity payment from principal, so deceased's bitcoin is not
  immediately remove from fund.
---

# Draft 3.0 - Drey Actuary Operations

## Introduction

To create a truly trustless bitcoin income plan, it is essential that Drey's actuarial models reflect the technical underpinnings that arise from operating in a decentralised manner from a technical perspective. The most critical point is the mechanics to ‘price’ participation and rewards in the fund, that they are easily understood if one were interrogating with a block explorer, while preserving fairness inspired by the nominal-gain methodology in Sabin and Forman (2016).&#x20;

Two methods of operation are novel in this respect.

Drey utilises [bitcoin inscription/ordinals](https://www.galaxy.com/research/whitepapers/bitcoin-ordinals-inscriptions-5-billion-nft-market/), so that records are public, (identities are masked), durable and immutable. In other words, Drey uses the bitcoin blockchain itself to store data decentralised actuaries will come to a consensus on, such as monthly distributions for the fund.

Drey allocates Dreybits to participants in the fund, which is a method to price participation and schedule distributions in an aggressively transparent, decentralised manner which preserves fairness for all participants.

### Bitcoin Ordinals and Inscriptions

Bitcoin inscriptions and ordinal theory have enabled bitcoin to be transformed into the world's most secure write once read only database.&#x20;

All manner of Mime types can be inserted into a bitcoin blob space intrinsically linked to a specific satoshi, making the data both immutable and transferable. As Drey Finance will be keeping records that last lifespans, and in order to reduce shared object storage complexities that will no doubt arise if miners use a DHT or off chain storage, Drey uses bitcoin as the shared object storage, exploiting the ordinals system for the following use cases:

* Monthly investor distributions schedule per fund to be agreed upon by the miners
* DAO proposals to be voted on by the miners
* Individual records pertaining to anonymous identity verification and authentication
* Individual records containing distribution information such as wallet address to send distributions
* Individual records containing general account information
* Proof of Life confirmation records
* New or updated actuarial models to be deployed
* New or updated R software models to be used in distribution calculations (TBD)

Documents generated for insertion into bitcoin storage will use a defined schema (TBC) on [JSON-LD documents](https://en.wikipedia.org/wiki/JSON-LD) compressed with [Briotli.](https://github.com/google/brotli) See the recommendations [here](https://www.lucidchart.com/techblog/2019/12/06/json-compression-alternative-binary-formats-and-compression-methods/).

The rest of this specification is described **in another section to be completed**.

### Voting

Any Drey miner can create a DAO proposal by generating the document, inscribing it at a particular satoshi, and relaying the satoshi ordinal value to any other miner over the [nostr protocol](https://nostr.com/). The voting request announcement and JSON-LD document should contain a block height of when the vote will occur. A supermajority of miners will be required to vote through any proposal, distribution schedule or other material decision. Distribution schedules are assigned tasks as described below.

Each JSON-LD document in the Bitcoin blockchain will contain an address to forward the satoshi to that represents a yes or no. The same will also be described in the nostr protocol vote request. The decentralised miner protocol will be used to create a transaction at x block height to move the satoshi to a specific wallet address denoting yes or no and declared in the nostr communication and the JSON-LD document, indicating whether an issue or schedule was agreed to or not.

## Dreybits

A Drey miner, selected by verifiable random function, proposes a monthly distribution schedule called a Dreybit ledger based upon the R software packages each miner runs to operate the fund. This proposed distribution schedule is written into the bitcoin blockchain at a specific satoshi and relayed to the miner population over nostr. The decentralised miner protocol will be asked to create a transaction at _x_ block height to move the satoshi to a specific wallet address conveying acceptance or rejection. Incentives for good behaviour and disincentives for bad behaviour are discussed in the **Drey tokenomics section**.

The Dreybit ledger contains each investor's allocated Dreybit amount to be received in each re-allocation cycle that occurs on the beginning of each month. Note that this is after an initial cycle at the initialisation of the fund at the beginning of month one. This process starts following the distribution of deceased member's Dreybits to survivors, and ultimately distribution of deceased member's bitcoin to surviving members which occurs at the end of the month.&#x20;

Each Dreybit ledger contains an alias ID created for the user during signup which maps to their bitcoin address and Dreybits allocated. The amount of Dreybits allocated depends on the investor’s probability of dying and amount invested (explained in a following section) relative to all investment in the fund.

The reason Dreybit ledgers must be re-updated monthly is to take into account variables such as the heuristics of the entire population at the beginning of the month since investors will move into new mortality rates as they age, previous investors pass away and are removed from the fund, new investors were added during the month, amounts invested as a pro-rata percentage of the entire value of the fund have changed, etc. These variables will change during the month, hence the allocated Dreybits to individual investor will change.

### Longevity Fund Terms and Conditions

Drey creates a set of binding smart contracts and terms and conditions which reflect the following stipulations that a longevity risk pooling fund inherits:

* The investors in the fund agree that upon their deposit of bitcoin, this investment is an irrevocable gift to all other present and living participants in the fund who have already joined or will join in the future.
* This gift passes in entirety to the living participants in the fund when the contributing investor passes away
* It is held in escrow in a smart contract
* An investor’s allocation of their Dreybits is revoked/cancelled if-and-when the unit owners pass away
* He/she continues to enjoy the benefit of holding those Dreybits as long as they continuously (monthly) provide proof that you he/she is alive within a certain time limit
* If such proof isn’t supplied, the rights conveyed by holding these Dreybits are forfeited, and ownership of the underlying bitcoin is distributed among those who did supply such proofs—that is they are still alive. This is a type of [tontine agreement](https://en.wikipedia.org/wiki/Tontine).

### Other Mechanics

* Individuals can continuously invest in the fund and be assigned Dreybits at the beginning of the month&#x20;
* Dreybits ARE NOT transferrable by action of the owner&#x20;
* They are transferrable by action of the smart contracts only
* Dreybits are calculated using satoshi as the base investment numbering system
* Yearly mortality rates are divisible by 12, to acclimate the rates to a monthly accounting.

## Dreybit Allocation Method

Dreybit allocation is specific to each individual user, so a scaling factor arises based on the the investor's probability of dying and their investment amount. For example, if an investor is 30 years old, a down scale occurs because their probability of living is much higher than a 65-year-old based on the actuarial data being used. This keeps the distributions fair via formulas inspired by the [nominal gain method](#user-content-fn-1)[^1].

Surviving members of a fair tontine do not receive equal allocations of each dying member’s forfeited balance.

Rather, they receive unequal allocations that depend on their respective mortality rate, _q_, and current account balance, _s_.

The intuition behind Dreybits and the allocation formulas are to maintain fairness on Dreybit distributions for everyone, regardless of your investment amount or life expectancy.

The allocation formula is as follows:

1. Determine the product of each individuals current balance in the fund in satoshi s with their mortality rate q. Acclimate a yearly mortality rate into a monthly one by dividing the yearly rate by 12.
2. Determine the sum all products for each individual together. &#x20;
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

The calculations are performed at the end of the month prior to new re-allocation exercise being performed.&#x20;

These Dreybits are mapped to the sum of all the deceased's bitcoin by determining the pro-rata percentage allotment to be inherited of the total deceased's Dreybits for the period.

$$p_{(1-ith)} = \frac{DBalloc(1-ith)}{\sum_d}$$

$$\sum dec(btc) = sum\, of\, decased's\, bitcoin$$

$$p*\sum dec(btc) = percentage\, of\, \sum dec(btc)\, distributed$$

Note that this operation _MUST_ remove the deceased's Dreybits and hence the underlying bitcoin from the original fund and distribute the bitcoin to the survivors. However, the survivors have a choice of receiving this distribution directly to a wallet under their control, or, they can elect to deposit the received bitcoin (and monthly airdrop of Drey) into a Drey savings/staking account, where the bitcoin and DREY tokens are deposited into a two-sided liquidity pool (DREY/bitcoin). This is explained in detail in the section on **Drey Savings accounts**.

### Monthly Annuity Payment

In version 3.0 of the protocol, rather than returning all of the deceased’s bitcoin every month to the survivors and emptying the sum of all deceased’s bitcoin out of the fund, the fund should redistribute the ownership of the bitcoin to surviving members but KEEP the bitcoin in the fund. A back of an envelope calculation sees that by doing so we greatly increase the bitcoin in the fund which drives an ever-increasing yield from the staking and mining operations. The individual investor will still experience an increase in their monthly distribution by way of the pro-rata assignment of deceased’s bitcoin to them which will also increase their ‘annuity like’ payment (from the remaining principal since their principal increases) and should increase their overall Dreybits allocation (unless perhaps there was a huge jump in new investors that month).

To determine the monthly payout, we use 120 as the age by which we expect all investors in the fund to live to for the USA, and for other locales we will use the last year by which mortality is expected to cease per that location's accepted mortality table. For the USA, we will use the 2012 IAM w/G2 scale for operations.

$$Annuity Factor = \sum [1 + _{n}p_{x} / (1+i)^n + _{(n+1)}p_{x} / (1+i)^{(n+1) }+_{(n+2)}p_{x} + ...]$$

$$_{n}p_{x}$$ where _x_ is the current age of the annuitant, _n_ is the time from the current age until projected death (in months), and _p_ is the probability of survival from the current age to the payment age, and _i_ represents the discount rate.

As mentioned, for an annuity paid for life the formula continues until it is assumed the person cannot live longer (typically 120 or so).

The payout of accumulated principal (after allocating mortality credits) at the end of the month is then to divide the principal by the annuity factor pay that amount out and reduce the principal accordingly. For example, assume an investor who starts the month with 100 BTC invested, earns an allocation of 2 BTC due to mortality credits to have 102 BTC in principal before the end of month payout. Also assume the investor is age 65 in 2024 and the discount rate is 5%. The corresponding monthly annuity factor is 160.773. The payout is then 0.634 (102 / 160.773) BTC and the remaining principal for the new month is 101.366 BTC.&#x20;

The nature of this methodology is all else being equal:

1. Higher assumed mortality rates (i.e., people expected to die sooner) means a greater payout rate.
2. Higher discount rates result in greater payouts as higher discount rates produce smaller annuity factors.
3. Older participants receive greater payouts than younger as their annuity factors are smaller.
4. Under typical mortality assumptions, men receive larger payouts than women of the same age as they are expected to die sooner.

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
7. Perform the APV of an Immediate Annuity formula to determine all fund investors' monthly payments by dividing the investors' principal by their annuity factor.
8. Distribute the monthly payments to all fund investors via bitcoin network and then remove that payment from the investors' tracked principal.
9. On the first of the month, re-run the Dreybit allocation steps and submit the re-allocation schedule for vote.
10. Obtain a positive vote on the re-allocation schedule.
11. Go to Step 3.

## References

Donnelly, C. (2015). Actuarial fairness and solidarity in pooled annuity funds. ASTIN Bulletin, 45(01):49–74.&#x20;

Donnelly, C., Guillén, M., and Nielsen, J. P. (2013). Exchanging uncertain mortality for a cost. Insurance: Mathematics and Economics, 52(1):65–76.&#x20;

Donnelly, C., Guillén, M., and Nielsen, J. P. (2014). Bringing cost transparency to the life annuity market. Insurance: Mathematics and Economics, 56:14–27.&#x20;

Forman, J. B. and Sabin, M. J. (2015). Tontine pensions. University of Pennsylvania Law Review, 173(3):755-831.&#x20;

Forman, J. B. and Sabin, M. J. (2016). Survivor funds. Pace Law Review, 37(1).&#x20;

Goldsticker, R. (2007). A Mutual Fund to Yield Annuity-Like Benefits. Financial Analysts Journal, 63(1):63–67.&#x20;

Gründel, H. and Wandt, M. (July 6, 2017). The modern tontine: An innovative instrument for longevity risk management in an aging society. ICIR Working Paper Series No. 22/2016.&#x20;

Kantorowicz, E. H. (1957). The King’s Two Bodies: A Study in Mediaeval Political Theology, Princeton University Press, Princeton, NJ, 411-412.&#x20;

Milevsky, M. A. and Salisbury, T. S. (2015). Optimal Retirement Income Tontines. Insurance: Mathematics and Economics, 64:91–105.&#x20;

Milevsky, M. A. and Salisbury, T. S. (2016). Equitable retirement income tontines: Mixing cohorts without discriminating. ASTIN Bulletin, 46(3):571-604.&#x20;

NAIC (2013). NAIC model rule (regulation) for recognizing a new annuity mortality table for use in determining reserve liabilities for annuities. National Association of Insurance Commissioners.&#x20;

Piggott, J., Valdez, E. A., and Detzel, B. (2005). The simple analytics of a pooled annuity fund. Journal of Risk and Insurance, 72(3):497–520.&#x20;

Sabin, M. J. (March 26, 2010). Fair tontine annuity. Available at SSRN: https://ssrn.com/abstract=1579932 or https://dx.doi.org/10.2139/ssrn.1579932.&#x20;

Sabin, M. J. and Forman, J. B. (November 9, 2016). The analytics of a single-period tontine. Available at SSRN: https://ssrn.com/abstract=2874160 or https://dx.doi.org/10.2139/ssrn.2874160.&#x20;

Stamos, M. Z. (2008) Optimal consumption and portfolio choice for pooled annuity funds. Insurance: Mathematics and Economics, 43(1):56–68.&#x20;

Waring, M. B. and Seigel, L. B. (2015). The Only Spending Rule Article You Will Ever Need. Financial Analysts Journal, 71(1):91–107.

[^1]: Forman, J. B. and Sabin, M. J. (2016). Survivor funds. Pace Law Review, 37(1).&#x20;
