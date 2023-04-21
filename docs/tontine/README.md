---
description: Draft 2.0
---

# Fair Tontine Calculations/Operations

## Fair Tontine Tontine Forfeiture Allocation

Surviving members of a fair tontine do not receive equal allocations of each dying member’s forfeited balance.

Rather, they receive unequal allocations that depend on their respective mortality rate, _q_, and account balance, _s_.

One useful property of this method is that it promotes transparency by being easily decomposed into two simple components: (1) a nominal tontine (life credit) yield for each member, which is easily obtained from the tontine’s mortality table, and, (2) a common adjustment factor that accounts for the difference between the amount of forfeitures experienced by the pool during a given period and the amount that was nominally expected, plus the amount expected from the investment yield.

A “nominal-gain method” described in Sabin and Forman (2016), which is desirable for its relative simplicity and explanatory properties can deliver this per “Tontines A Practitioner's Guide to Mortality-Pooled Investments.pdf” (page 12).

## How Drey Works

Due to regulatory risk, it’s imperative that our models reflect the actual way that we will work from a technical perspective, and the way we ‘price’ participation in the tontine is easily understood while preserving fairness. We will also be exploiting [bitcoin inscription/ordinals](https://www.galaxy.com/research/whitepapers/bitcoin-ordinals-inscriptions-5-billion-nft-market/), so that records are public, (identities are masked), durable and immutable. In other words, we will be using the bitcoin blockchain itself to store data decentralised actuaries will come to a consensus on, such as monthly distributions for the fund.

### Terms and Conditions

What Drey will do is create a set of binding smart contracts and terms and conditions which reflect the following stipulations:

* The investors in the fund agree that upon their deposit of bitcoin, this investment is an irrevocable gift to all other present and living participants in the fund who have already joined or will join in the future.
* This gift passes in entirety to the living participants in the fund when the contributing investor passes away.
* It is held in escrow in a smart contract until then, with the smart contract issuing monthly payments based on a fraction of principal calculated using the maximum life date based on actuarial data.

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

The Dreybit ledge contains each investors allocated bitcoin amounts to be received in the next distribution. Each Dreybit ledger alias ID is created for the user during signup which maps to their bitcoin address and amount of bitcoin to be received. The amount of bitcoin an investor gets depends on the investor’s probability of dying and amount invested (explained in a following section) relative to all&#x20;

At the end of every month, a new Dreybit ledger is created with updated Dreybits allocated to all investors. Ledgers must be updated to take into account the heuristics of the entire population at the beginning of the month (has the weighted average of year of dying moved) since new investors were added during the month, amount invested as a pro-rata percentage of the entire value of the fund and the base price differential formula (explained below).

An investor’s allocation of their Dreybits is revoked/cancelled if-and-when the assignees pass away.

* He/she continues to enjoy the benefit of holding those Dreybits month to month as long as they continuously (monthly) provide proof that you he/she is alive within a certain time limit.
* If such proof isn’t supplied, the rights conveyed by holding these Dreybits are forfeited, and ownership of the underlying bitcoin is distributed among those who did supply such proofs—that is they are still alive. This is a type of tontine agreement.
* All Dreybits are unique and are tied to individual Satoshi using the bitcoin Ordinal & Inscription method.
* A Dreybits assignment certificate (NFT) is imprinted into the bitcoin blockchain at a unique Satoshi identity and cryptographically bound to the investor. In essence, this is an NFT on the bitcoin blockchain signifying the investor’s temporary assignment of a unique Dreybit certificate and the exact amount of Dreybits this certificate describes as assigned to the investor. It is analogous to a uniquely issued bearer bond.
* The certificate is on the bitcoin blockchain, so it never needs backup.
* A Drey mobile app is used to verify the cryptographic attestation that a particular individual is granted a Dreybits assignment certificate to him/her (explained in a following section) by way of a zero-knowledge proof of identity. This is done using the M-Pin protocol.
* An embedded M-Pin server key and GUID reside in the certificate to enable an Oracle service to run the protocol and validate Proof of Life. The M-Pin client key is backed up by the investor using a simple 12-word mnemonic (or easier method).
* The Oracle Proof of Life Service only records the GUID ID, date of birth, sex, geography (mortality table) and Dreybits under ownership for each user and never permanently stores identity information like name, email, address, etc.
