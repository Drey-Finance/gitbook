---
description: Drey's decentralised actuarial operating system explained.
---

# Architecture IV

## Server-Side Proof Network

Drey Finance has in inbuilt server-side proof network. Proof networks are prover sets that service a single application, like a validity rollup. In Drey Finance’s case, the application is Dreybits monthly allocation formula calculation. We want to know that it has been performed correctly according to the prescribed formula. Drey Finance’s proving operations are decentralized. In doing so, we gain:

* Liveness: Multiple provers ensure that the protocol operates reliably and doesn’t face downtime if some provers are temporarily unavailable.
* Censorship Resistance: Having more provers improves censorship resistance. A small prover set could refuse to prove certain types of transactions.
* Competition: A larger prover set can strengthen market pressures for operators to create faster and cheaper proofs.

In addition, by Drey Finance having its own on-board prover network it obtains greater sovereignty than outsourcing the proof generation and verification, so rather than creating an external point of failure it removes it.

Introducing multiple provers to a protocol creates additional complexity for the network. It is the tradeoff for censorship resistance, liveliness and generating market pressure to create fast proofs and verifications. A primary challenge being the protocol must decide which prover is assigned to perform the Dreybit allocation formula for the time period, and how to de-risk relying on one zero knowledge prover or verifier. Thanks go to [Figment Capital](https://figmentcapital.medium.com/decentralized-proving-proof-markets-and-zk-infrastructure-f4cce2c58596) for creating a taxonomy around 3 main approaches:

* Stake-based prover selection — Provers stake assets to participate in the network. At each proving slot, a prover is selected at random, weighed by their value of staked tokens, and computes the output. Provers are compensated for producing a proof when chosen. Specific slashing conditions and leader selection can be different for each protocol. This model is similar to Proof of Stake.
* Proof mining — Provers are tasked with repeatedly generating ZKPs until they generate a proof with a sufficiently rare hash. Doing so earns them the right to prove at the next slot and earn the slot reward. Provers that can generate more ZKPs are more likely to win the slot. This type of proving closely mirrors PoW mining — it is energy and hardware intensive. A key difference with traditional mining is that in PoW, hashing is merely a means to an end. Being able to produce SHA-256 hashes in Bitcoin has no value beyond increasing the network’s security. In proof mining however, the network provides incentives to miners to accelerate ZKP generation.
* Proof racing — At each slot, provers compete to produce a proof as quickly as possible. Whoever generates the proof first receives the slot reward. This approach is vulnerable to winner-takes-all dynamics. If a single operator is able to generate proofs faster than anyone else, they should win every slot. [Centralization can be reduced](https://ethresear.ch/t/proof-of-efficiency-a-new-consensus-mechanism-for-zk-rollups/11988/6) by splitting up the proof reward across the first _n_ operators who generate a valid proof or introducing some randomness into which proof is accepted. Yet even in this case, the fastest operator can simply run multiple machines to capture the other revenue.

Drey Finance incorporates elements of both Stake-based prover selection and Proof racing, accentuating the benefits of both but limiting the downside of proof racing’s centralisation.

### Network Operations&#x20;

Drey Actuary clients, to qualify as an eligible client to participate in the Dreybits allocation formula protocol must have a minimum amount of bitcoin staked within the system. Every month, from the available pool of Actuary Clients, a distributed verifiable random function protocol is run between all Actuary Clients who meet the levels of bitcoin staking necessary to become active Actuary Client helping to secure the network. Running the distributed verifiable random function protocol selects the Lead Actuary at random for the monthly period but draws the Lead Actuary from a qualified pool of Actuary Clients based on the level of bitcoin deposits they have staked within the main Vault wallet itself.&#x20;

Additionally, there is a role for all Actuary Clients who meet the minimum bitcoin staking threshold to participate in the protocol as ‘Secondary’ Actuary Clients, de-risking a possibility that a malicious Actuary Client could be chosen for the Dreybits allocation formula protocol. Further, there are in place incentives and disincentives for collusion between Actuary Clients to achieve anything but a proper result.

How the Lead Actuary calculates the new monthly Dreybits allocation is covered in the section [Dreybits Allocation Method](../docs/Operations.md#dreybit-allocation-method). Dreybits monthly allocation tables are built and stored in the bitcoin blockchain as Parquet files. [Parquet](https://parquet.apache.org/docs/overview/motivation/) is a columnar data format that is designed for efficient data storage and retrieval. Parquet files are smaller than CSV files, and they can be read and written much faster. Parquet files also support nested data structures, which makes them ideal for storing complex data, and compression, which enables efficient use of space within the bitcoin blockchain.

Each row in the Parquet file includes a hash of all the concatenated data in the row and this hash serves as the leaf in a Merkle tree. When the entire table is updated, the Dreybits allocation column will change as each value in that cell will change for all existing rows and obviously new rows (as new Drey plans are created for new users).

So, for example, the row would contain at a minimum:

_Month | UserID | Dreybits Allocation | h(Time Period | UserID | Dreybits Allocation)_

Each new update of the table changes at least the Month and Dreybits Allocation cells, changing the hash of the concatenated data at the end of the row.

This hash serves as the leaf in a Merkle tree that represents that month resulting in a new root for each month. In other words, for each new month in the table, an entirely new Merkle tree with a new root node is created.

This root node then serves as a leaf in another Merkle tree creating a relationship between months.

INSERT GRAPHIC HERE

Using zkWASM, we can run a purpose built WASM binary inside the zkWASM VM which takes an existing Merkle tree data structure (the one representing the current month), forms a new leaf (representing the current upcoming monthly distribution) as the input, and outputs a new Merkle tree root along with a zero-knowledge proof that the new Merkle tree root was computed correctly.

To derive the zero-knowledge proof, the code that calculates the output of the Merkle tree is a self-contained WASM binary loaded up as a plug-in to the Drey Actuary client application, and then run inside a zkWASM virtual machine embedded within the Drey Actuary client software application. The WASM binary is small size. By embedding the WASM binary that calculates the Dreybits allocation formula into the bitcoin blockchain, any Dreybit Actuary client, or indeed anyone with access to the bitcoin blockchain, can verify the WASM binary’s data integrity, correct version and data availability.

INSERT GRAPHIC HERE

The result is a zero-knowledge proof, verifiable by anyone running a zkWASM virtual machine, which proves the new root nodes of the Merkle tree were calculated correctly.&#x20;

To finalise the new Dreybit monthly allocation table, the Lead Actuary for the month creates a bitcoin inscription transaction embedding a digitally signed binary data package into the bitcoin blockchain. The binary data includes the new Dreybits monthly allocation column, the new root node value and the zero knowledge proof of correct computation of the new root node value.&#x20;

With this data inserted as an inscription in the bitcoin blockchain, any Drey Actuary client, even one that is not participating in the allocation calculation protocol, can recalculate on their own the Dreybits monthly allocation table using the WASM binary loaded into the Actuary Client which is retrieved out of the bitcoin blockchain at a specific satoshi (an inscription with binary data). In this way, the Actuary Client serves a light client, able to verify that the Dreybits allocation formula was adhered to with a proof of correct calculation.&#x20;

## Game Theory

### Naive Approach

The naive approach outlined above, on its own, still leaves gaps where a malicious Actuary Client could fake additional data into the calculation set, pass it off as legitimate, and calculate an inaccurate allocation distribution result. In other words, the security and censorship resistance of this naive approach depends on the likelihood of having an honest node drawn from the verifiable random function producing lottery. What is required here is to have a collection of incentives and disincentives that punishes malicious behaviour and incentivizes honest participation of a group of Actuary Clients in verifying the monthly allocation distribution result to achieve liveliness and correctness via a competitive incentive.

This is achieved by having a super majority of Actuary Clients compete to also calculate the Dreybits monthly allocation formula, produce on their own the new root node and zero knowledge proof of correct computation of the new root node, and create an inscription (taproot transaction) that embeds a digitally signed data package that contains their calculated new root node and their calculated zero knowledge proof of correct computation into the bitcoin blockchain. They do not need to include the new Dreybits allocation column, as the Lead Actuary has already embedded this column into their data package, and a correct result of the column will result in the same root node being produced for everyone. The idea behind this action is that all Secondary Actuary’s validate the Lead Actuaries monthly Dreybit allocation result.

This approach, while better, doesn’t provide a sufficient safeguard against a lazy Actuary Client inadvertently providing help to a malicious Actuary Client.&#x20;

A digitally signed zero knowledge proof and new root node does not prohibit the lazy Actuary Client from copying the new root node and zero knowledge proof out of the bitcoin mempool, remove the digital signature, sign the new root node and zero knowledge proof as their own calculations, formulating a transaction (inscription) embedding these values and sending it to the network. The interloper will have done no real work and will have bolstered a malicious actor’s chance of succeeding.

### Commitment Scheme

The solution here is to employ a threshold encryption scheme among all eligible Actuary Clients involved in the protocol. Specifically, the [Pallier threshold encryption scheme](ttps://eprint.iacr.org/2023/998.pdf).

Each Secondary Actuary Client participating in the protocol will calculate the new Dreybits monthly allocation on their own, and generate a new root node and zero knowledge proof of correct computation of the root node. Each Actuary Client, including the Lead Actuary, encrypts their new root node and zero knowledge proof to the public key of a threshold Pallier encryption. Only a threshold (majority) of Actuary Clients working together will be able to decrypt the encrypted data packages once they are placed into the bitcoin blockchain. The Actuary Clients will only run the collective decryption routine once a majority of Actuary Clients have placed their encrypted data packages in the bitcoin blockchain.

By having all Actuary Clients encrypt their data packages, this action negates any possibility of a lazy Actuary Client providing help to a malicious Actuary Client through the protocol itself, as all data that everyone is must attest to as correct is in fact encrypted, creating a commitment scheme.&#x20;

Because the data package to be encrypted includes the digital signature of the Actuary Client creating the encrypted data package, the encryptions themselves will be worldly unique. In other words, copying the Lead Actuaries encrypted data package as your own will fail as it will become evident that the data package does not contain the correct digital signature from the individual Actuary Client once decrypted.

This encryption to the Pallier threshold public key also applies to the Lead Actuary client performing the initial calculations. The difference is the Lead Actuary also encrypts the new Dreybit Allocation column with the new Dreybits allocation amounts also with the Pallier threshold public key. The result is that all data packages inserted as an inscription into the bitcoin blockchain on this initial step, from the Lead Actuary’s to the Secondary Actuary’s data packages are encrypted in a way that only a majority of Actuary Clients operating together can decrypt the data. Again, the difference between the Lead Actuary’s encrypted data package and the Secondary Actuary’s encrypted data packages is that the Lead Actuary includes the new monthly Dreybit allocation column from the table, in addition to the new root node and zero knowledge proof of correct computation of the new root node. The Secondary Actuary’s encrypted data packages contain only their calculated new root node and their calculated zero knowledge proof of correct computation of the new root node.&#x20;

INSERT GRAPHIC HERE

Note that in the event the Lead Actuary does not make a calculation and post the inscription to the bitcoin blockchain in a determinate amount of time, the verifiable random function lottery will be run again to select a new Lead Actuary. Not responding to the call to perform as Lead Actuary to calculate the new monthly Dreybits allocation distribution table will result in a penalty to reputation or possible monetary (via slashing bitcoin deposit and redistributing it to the fund depositors). Additionally, a penalty mechanism will be in place for a Lead Actuary that purposefully inserts junk or incorrect calculations into the bitcoin blockchain.

The Secondary Actuary Clients will only begin a proof race to confirm the Lead Actuary’s calculations after the sixth confirmation block is finalised containing the Lead Actuary’s encrypted data package. Then the ‘race’ between the Secondary Actuary Clients begins.&#x20;

INSERT GRAPHIC HERE

As described above, Secondary Actuaries who have staked enough bitcoin into the Drey Fund to help secure the protocol can then input their encrypted data packages into the bitcoin blockchain. The protocol incentivizes good behaviour, liveliness, security and speed by dividing up the AUM fees collected for the month off the total deposit base between the Lead and Secondary Actuaries participating in the protocol. The Lead Actuary (determined by stake and probability) takes the largest percentage of the protocol’s revenue for the month, followed by the Secondary Actuaries confirming the Lead Actuary’s monthly Dreybit allocation calculations.&#x20;

The ‘race’ between Secondary Actuaries is to see who can submit their transactions to the bitcoin blockchain in a way that orders their transactions first and/or before other Secondary Actuary Client’s transactions in the seventh block after the Lead Actuary’s encrypted data package is finalized. The Secondary Actuary who has the first transaction in the seventh block after the Lead Actuary’s transaction receives the second highest award for securing the protocol after the Lead Actuary. This transaction does not need to be first in the block, it merely needs to be first among all Secondary Actuary’s competing in the proof race. The Secondary Actuary who has the next transaction in the seventh block receives the third highest award, and so on. This continues until a majority of Secondary Actuaries populate the seventh block and this block is then confirmed six times itself.

INSERT GRAPHIC HERE

It’s only then that the new Dreybits monthly allocation calculation, the new root node and zero knowledge proof of correct computation of the new root are revealed for both the Lead Actuary Client’s encrypted data package and the Secondary Actuary Clients who have embedded their calculated new root node and zero knowledge proof of correct computation into their encrypted data packages and inscribed them into the bitcoin blockchain. In order for the Dreybit monthly distribution allocation result to be accepted, upon the decryption of all values, a super majority of Dreybit Actuaries must have agreed on the same allocation result (the new Merkle tree root) as the Lead Actuary, and each must have produced a proof of correct computation.

As a final step, the new Dreybit monthly allocation column (which enables the buildup of the table) is written into the bitcoin blockchain as an inscription, but this time in plaintext. The transaction is created by the Drey Actuaries using the [Drey Voting protocol](../docs/Operations.md#drey-voting-protocol).

## Tidying Up

Using a full Bitcoin Core node with txindex and RPC enabled, all blocks and transactions can be queried. This is done by querying the blockhash for every block number. Subsequently, by using this blockhash, the block of transactions is retrieved. Then for every transaction hash in the retrieved block, the raw transaction is queried and decoded.&#x20;

Date of creation is not necessary because the blockheight of the block the initial enrolment transaction is in can tell you when the account was created.&#x20;

Amount on deposit is not necessary because the Deposit Address can be looked up amongst all transactions within bitcoin to tell you what the account balances are within each account.

The intention is to limit the data put into the bitcoin blockchain to that data which is critical foundation data about the fund depositor but from which other profile data can be built up around it. As an example, a ‘date of creation’ field is not necessary to embed into the bitcoin blockchain because the time when initial funding tx was recorded into the bitcoin blockchain is discernible from the block height of the block where the initial funding tx is embedded.

Using the Parquet file system delivers efficiencies. Data can be sharded by column, so producing a new Dreybits allocation table in totality is not necessary.&#x20;

A regular SQL database can be built up from a local bitcoin blockchain indexer (such as chainhooks) which interrogates the transactions in each block from the 1st block containing a new customer.

All that is needed in a Parquet file for a complete picture is:

_UserID | DoB | Geography | Sex | Dreybits | Deposit Address | hash of all concatenated items._

However, when a user is first injected into the system, they will not have Dreybits yet so their data looks like this:

_UserID | DoB | Geography | Sex | Deposit Address_

Mortality rates get updated as mortality tables change and as users age so there is no use in putting that data into the bitcoin blockchain as it is ephemeral and changing.
