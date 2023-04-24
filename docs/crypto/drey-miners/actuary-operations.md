# Actuary Operations

## Introduction

To create a truly trustless bitcoin income plan, it is essential that Drey's actuarial models reflect the technical underpinnings that arise from operating in a decentralised manner from a technical perspective. The most critical point is the mechanics to ‘price’ participation and rewards in the fund, that they are easily understood if one were interrogating with a block explorer, while preserving fairness inspired by the nominal-gain methodology in Sabin and Forman (2016).&#x20;

Two methods of operation are novel in this respect.

Drey utilises [bitcoin inscription/ordinals](https://www.galaxy.com/research/whitepapers/bitcoin-ordinals-inscriptions-5-billion-nft-market/), so that records are public, (identities are masked), durable and immutable. In other words, Drey uses the bitcoin blockchain itself to store data decentralised actuaries will come to a consensus on, such as monthly distributions for the fund.

Drey allocates Dreybits to participants in the fund, which is a method to price participation and schedule distributions in an aggressively transparent, decentralised manner which preserves fairness for all participants. Dreybits are not DREY tokens. Dreybits are an accounting method to determine fair distributions and payouts internal the Drey accounting system but transparent and visible within the bitcoin blockchain.

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

## Voting

Any Drey miner can create a DAO proposal by generating the document, inscribing it at a particular satoshi, and relaying the satoshi ordinal value to any other miner over the [nostr protocol](https://nostr.com/). The voting request announcement and JSON-LD document should contain a block height of when the vote will occur. A supermajority of miners will be required to vote through any proposal, distribution schedule or other material decision. Distribution schedules are assigned tasks as described below.

Each JSON-LD document in the Bitcoin blockchain will contain an address to forward the satoshi to that represents a yes or no. The same will also be described in the nostr protocol vote request. The decentralised miner protocol will be used to create a transaction at x block height to move the satoshi to a specific wallet address denoting yes or no and declared in the nostr communication and the JSON-LD document, indicating whether an issue or schedule was agreed to or not.

## Dreybits

A Drey miner, selected by verifiable random function, proposes a monthly distribution schedule called a Dreybit ledger based upon the R software packages each miner runs to operate the fund. This proposed distribution schedule is written into the bitcoin blockchain at a specific satoshi and relayed to the miner population over nostr. The decentralised miner protocol will be asked to create a transaction at _x_ block height to move the satoshi to a specific wallet address conveying acceptance or rejection. Incentives for good behaviour and disincentives for bad behaviour are discussed in the **Drey tokenomics section**.

The Dreybit ledger contains each investor's allocated Dreybit amount to be received in each re-allocation cycle that occurs on the beginning of each month. Note that this is after an initial cycle at the initialisation of the fund at the beginning of month one. This process starts following the distribution of deceased member's Dreybits to survivors, and ultimately distribution of deceased member's bitcoin to surviving members which occurs at the end of the month.&#x20;

Each Dreybit ledger contains an alias ID created for the user during signup which maps to their bitcoin address and Dreybits allocated. The amount of Dreybits allocated depends on the investor’s probability of dying and amount invested (explained in a following section) relative to all investment in the fund.

The reason Dreybit ledgers must be re-updated monthly is to take into account variables such as the heuristics of the entire population at the beginning of the month since investors will move into new mortality rates as they age, previous investors pass away and are removed from the fund, new investors were added during the month, amounts invested as a pro-rata percentage of the entire value of the fund have changed, etc. These variables will change during the month, hence the allocated Dreybits to individual investor will change.

_**NOTE: Dreybit ledgers v 1.0 may use the bitcoin blockchain 'blob' space to record individual investor's Dreybit allocation, but v 2.0 'could' use the Taro upgrade to issue Dreybits as assets on the Bitcoin blockchain if/when the Taro upgrade takes place.**_

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

## Dreybit Allocation Method - REVIEW/SIMULATIONS IN PROCESS
