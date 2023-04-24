# Request for Quote

Hopefully, from the very rough descriptions in the preceding sections, a picture emerges of innovations necessary to bring this vision to reality.

Drey Financial is looking for a development partner/team that can respond to this RFQ and supply a fixed quotation on a project by project basis for the following work streams. Note that these work streams are not an exhaustive list of software engineering projects necessary to bring the platform to production. The intention is to use the deliverables of key innovation as a proof point for seed round fundraising.

## Work stream 1

The initial work stream will create a software implementation of the FROST/ROAST DKG and transaction signing inside of nostr joint client/gateway instances that enable asynchronous communication necessary to achieve a threshold signature between _t_ out of _n_ instances utilizing the nostr communication protocol.&#x20;

The final deliverable should be a working demo that shows at least 20 different instances (can be containers on the same machine) co-ordinating a DKG to ultimately create a Schnorr derived P2TR wallet address (this should enable including multiple customized redeem scripts to choose from in order to spend the bitcoin later) and then co-operatively signing a 'dummy' transaction. The transaction is 'hard coded' in the demo, and not submitted.

The software will be written in Rust, and be able to be compiled from source to both target OS (Windows, Linux, Mac) and most importantly a WASM binary. The target WASM runtime will be [WASMtime](https://wasmtime.dev/). Ideally, a optional estimate should be provided that enables the application to run in the [Lunatic runtime](https://lunatic.solutions/).

The software should have both a command line interface and web browser interface. The UI should be simple, clean, intuitive and branded in Drey Finance iconography and colour scheme.

The code should be well documented, with appropriate units tests, compiling instructions, etc. While the quality does not have to be shippable, it does have to be of sufficient quality that would enable other open source developers to attach to the project and bring it into production ready state with reasonable ease. All work should take place in a Drey Finance GitHub repository under the MIT license.

## Work stream 2

Modify the developing implementation of the [Stacks Degen decentralized mining protocol](https://stacks-degens.gitbook.io/decentralized-mining-pool/) so it utilizes the software from Work stream 1 as the basis for its miner to miner communication to produce P2TR wallet addresses and signatures.

## Work stream 3

Extend the deliverable from Work stream 2 to incorporate [Chainhooks](https://www.hiro.so/blog/meet-4-new-features-in-clarinet?ref=stacksblog) Rust library, and read/respond to events from the bitcoin blockchain/Stacks blockchains, the Web UI **and** the nostr communications protocol. The use final deliverable should handle a mix of read/write events to Stacks, Bitcoin and nostr. A working demo should encapsulate the following:

* Create a trigger action, based on predicate that listens to the Bitcoin blockchain, that generates a transaction that moves bitcoin from the on-boarding wallet to the Drey Miner's BTC Vault on the condition that the Drey Proof of Life (onboarding) service layer has co-signed the transaction. This transaction should be formed by the extended Chainhook Rust library. A (PSBT) un-signed transaction circulated on nostr by the Drey Miners (avoid race conditions) as the 'thing' to sign, runs the ROAST implementation and signs the transaction, and is submitted to the Bitcoin blockchain.
* Through the Web UI, create a Drey Improvement Proposal, write the DIP into the Bitcoin blockchain as a Drey ordinal, note the Satoshi, circulate the location for a vote on nostr.
* Create a trigger action, based on predicate that listens to the nostr protocol, that prompts a user through the CLI and Web UI to review a DIP, and vote yes or no. Voting yes or now follows the workflow outlined in previous section (move the Satoshi to a specific yes/no wallet address).
* Other trigger actions TBD.

