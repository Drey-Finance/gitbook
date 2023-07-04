---
description: Drey's decentralised actuarial operating system explained.
---

# Architecture I

## Actuarial Operating System

Drey Finance's Actuarial Operating System is a unique, decentralized system that facilitates the operation of actuarial models and collaborative computations over the [Nostr protocol](https://nostr.com/) leveraging [CRDTs](https://crdt.tech/), provides data permanence and immutability via the [Bitcoin blockchain](https://bitcoin.org/en/), and leverages the ability to produce zero knowledge proofs of correct computation via [zkWASM](https://github.com/DelphinusLab/zkWasm). It fundamentally serves as a mechanism for the management and execution of actuarial tasks, leveraging the benefits of blockchain technology - such as transparency, immutability, and decentralization - to enhance the accuracy and reliability of actuarial operations. The Drey Finance Actuarial Operating System is designed to enable the calculation of life expectancy, risk management, and financial forecasting in a decentralized and collaborative manner. It employs Bitcoin's blockchain as a universal ledger, storing actuarial models, payout schedules, source code, proposals, and vote records, thereby ensuring data immutability, durability, transparency, trust and accessibility​​.

Importantly, Drey Finance's Actuarial Operating System is **not** a blockchain or Layer-2 protocol. While it leverages the Bitcoin blockchain and its own decentralized zero knowledge prover network for its functionality, it does not constitute a separate blockchain or protocol in its own right. Instead, it operates within the existing Bitcoin infrastructure, using these systems as a basis to carry out its specialized actuarial functions. It does not possess its own consensus mechanism, but instead uses the consensus mechanisms inherent in Bitcoin and Stacks to secure its operations. This ensures that it maintains the high level of security and decentralization associated with these established networks, while still facilitating the unique operations necessary for actuarial computations.

The Actuarial Operating System is an innovative application of blockchain technology to the field of actuarial science. Its design and function reflect the potential for blockchain technology to revolutionize industries beyond finance, including insurance and risk management. By operating within the established infrastructure of Bitcoin and leveraging a decentralized zero knowledge proving network, leveraging open standards like Nostr and CRDTs, it is able to capture the benefits of these systems while avoiding the complexities and risks associated with creating a new blockchain or protocol. This approach not only enhances the reliability and security of actuarial operations but also demonstrates the potential for blockchain technology to be used as a foundation for a wide range of applications, extending far beyond its original use as a digital currency.

## Bitcoin's Universal Ledger

The advent of [Taproot-type](https://trustmachines.co/learn/bitcoin-taproot-upgrade-basic-breakdown/) transactions has ushered in a new era for the Bitcoin Blockchain, fundamentally transforming its capabilities. Previously, the Bitcoin network was primarily used as a decentralized digital currency, with its data format being somewhat limited. However, with Taproot-type transactions, it is now possible to embed any type of data into the Bitcoin Blockchain. This means that the Bitcoin network can now serve as a universal ledger, capable of storing a wide variety of data types, not just transactional information. This opens up a plethora of new possibilities for developers and users alike, extending the utility of the Bitcoin network beyond its original purpose.

Once data is embedded into the Bitcoin Blockchain via a Taproot-type transaction, it becomes a permanent fixture on the network. This permanence is a key feature of the Bitcoin network, ensuring that once data is added to the blockchain, it cannot be altered or removed. This immutability provides a robust level of security and trust, as users can be confident that the data they see on the blockchain is accurate and has not been tampered with. This feature is particularly valuable in applications where data integrity is paramount, such as in legal contracts, property deeds, academic records, and actuarial operations.

In addition to permanence, data embedded into the Bitcoin Blockchain via Taproot-type transactions also inherits other key features of the Bitcoin network, such as availability and determinism. Availability ensures that the data is always accessible to anyone on the network, regardless of their geographical location or the time of day. This global accessibility is a cornerstone of the decentralized nature of the Bitcoin network. Determinism, on the other hand, ensures that the outcome of any transaction is predictable and consistent, regardless of when or where it is executed. This feature is crucial for the reliable operation of smart contracts and other automated processes on the blockchain. Together, these features make the Bitcoin network a powerful platform for a wide range of applications, far beyond its original use as a digital currency.

As described in following sections, Drey Finance leverages Bitcoin as a universal ledger, storing actuarial models, payout schedules, source code, proposals and vote records and more inside the Bitcoin blockchain. Bitcoin's features of data permanence, accessibility and determinism are unmatched by other distributed storage models available. By undertaking the goal of decentralizing actuarial operations, Drey Finance itself is held to a higher standards where longevity of data immutability, durability and accessibility will be measured across lifetimes. We believe Bitcoin as a universal ledger enables this vision to become reality.

## Understanding WASM and zkWASM

[WebAssembly (WASM)](https://webassembly.org/) is a virtual machine used in web development, allowing developers to program in various languages and compile them into the universal target of a WASM binary. It can run on different devices, such as smartphones, laptops, Raspberry Pis, and servers. Its efficiency, portability, and compatibility with popular programming languages make it a favorite among developers.

[zkWASM](https://github.com/DelphinusLab/zkWasm), on the other hand, is a computational proof generator that enables developers to verify a computation has been executed correctly without re-running the computation. This trustless method of computation is a game-changer for blockchain technology.

zkWASM offers infinite possibilities by allowing any type of computation to be performed trustlessly off-chain. With zkWASM, developers can use validity proofs to scale computational capabilities without having to trust third-party providers.

Additionally, zkWASM is portable. Portability means that zkWASM has the potential to be run on any kind of platform due to its native universality. zkWASM does still require a large RAM and a high-strength GPU and without further acceleration it cannot yet fully compete with its cousin WASM which runs basically everywhere. However, these hardware requirements do not place it out of the reach of most validators or miners participating in web3 ecosystems.

With the support of a strong community and a vast ecosystem, zkWASM has the potential to revolutionize the blockchain space. Projects such as Hyper Oracle, Delphinus Labs, Ankr, zkCross, and Dfinity are already working on zkWASM implementations.

Possible use cases for zkWASM include oracles, off-chain computation, automation, web2 meets web3, and proofs for machine learning models or data processing. As more developers and projects adopt zkWASM, its impact will scale the possibilities of web3 and open the doors to web2 developers.

In the following sections, we explain how Drey Finance uses zkWASM in a decentralized zero knowledge proof network to secure and make transparent fund management operations.



