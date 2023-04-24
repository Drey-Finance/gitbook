---
description: Describing the smart contracts on Stacks
---

# Smart Contracts

Smart contracts will be deployed to Stacks that have multiple tasks. A primary smart contract keeps track of the Drey Miners of the mining pool and their stakes of bitcoin and DREY tokens. Like the [decentralized mining protocol smart contract being built by Stacks Degen for Stacks blockchain](https://stacks-degens.gitbook.io/decentralized-mining-pool/smart-contract/overall-explanations), one Drey smart contract will organize the Drey miner population:

* Add new Miners to the mining pool through the Miners voting system. Utilizing Chainhooks, a satoshi containing the instructions to add a new miner sent to a wallet address signifying a yes vote would trigger the function to add a new miner.&#x20;
* The Miners will be able to vote to remove existing Miners in the case of them being bad actors

Another smart contract will keep track of the STX, BTC, DREY token balances each Miner has staked into Alex protocol, Zest protocol or other yield bearing mechanism and enable a threshold to release miner's funds.

Another smart contract will control the issuance of DREY tokens on the Stacks blockchain, incentivizing Drey fund depositors.
