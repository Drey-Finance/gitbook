---
description: Drey's decentralised actuarial operating system explained.
---

# Architecture III

## Drey Actuary Client

The Drey Actuary Client is a software component developed in Rust, which interfaces with the Drey Finance system and the underlying blockchains, Bitcoin and Stacks. This open-source project, licensed under Apache 2.0, ensures reliable access to the Bitcoin and Stacks blockchains, essential for the Drey Finance system's operations.

The client's functionality includes integration with the Bitcoin client RPC-API and the Stacks API. This integration allows direct interaction with the blockchains for operations such as transaction submission and data retrieval. The ability to interact with these APIs provides necessary infrastructure for the Drey Finance system to operate efficiently on these blockchains.

The Nostr protocol, a decentralized communication protocol, is a key feature of the Drey Actuary Client. It ensures secure and efficient communication between different instances of the software, providing the synchronous communication required for the coordination of operations within the Drey Finance system.

For data synchronization and replication, the Drey Actuary Client uses Conflict-free Replicated Data Types (CRDTs). CRDTs are data structures that permit independent and concurrent updates of multiple replicas without data conflicts. The implementation of CRDTs ensures that all instances of the Drey Actuary Client maintain consistent data, contributing to the integrity and reliability of the Drey Finance system.

Finally, the Drey Actuary Client is equipped with an event observer. This feature allows the software to respond programmatically to events on the Bitcoin and Stacks blockchains. It enables the Drey Actuary Client to monitor these blockchains for specific occurrences and initiate predefined actions in response. This capability is crucial for the real-time, automated processes within the Drey Finance system. Further details and opportunities for contribution can be found on the Drey Actuary Client project's GitHub page at [https://github.com/Drey-Finance/actuary-client](https://github.com/Drey-Finance/actuary-client).

## CRDTs

CRDTs, or [Conflict-Free Replicated Data Types](https://en.wikipedia.org/wiki/Conflict-free\_replicated\_data\_type), are a class of data structures that are uniquely designed for multi-user applications. They were introduced in [2011 in academic computer science research](https://pages.lip6.fr/Marc.Shapiro/papers/RR-7687.pdf). Like standard data structures such as hash maps and lists, CRDTs can store document state, but with the added feature of handling multi-user interactions right from the ground up. They are designed to tolerate concurrent updates from different users and to resolve conflicting updates without requiring any central authority or consensus mechanism. Essentially, CRDTs allow multiple replicas of the same data to be updated independently and concurrently, and yet eventually converge to a consistent state.

In the context of the Drey Finance Actuary Client, CRDTs are used to store, manage and communicate different types of data across the network. One of the key applications is implementing [Nostr events](https://nostr.com/the-protocol/events) as [different data types](https://redis.com/blog/diving-into-crdts/). [Nostr](https://nostr.com/) is a protocol designed for creating and handling shared events across a network, and it's a perfect match for the decentralized nature of Drey's actuarial operations. Nostr events can represent a variety of data types, such as proposals, actuarial models, private conversations, and partially signed bitcoin transactions. Each of these data types corresponds to a specific action or task performed by the actuarial operating system, and using Nostr events allows these tasks to be communicated and processed in a decentralized way.

The choice to use CRDTs and Nostr events within the Drey Finance Actuary Client is rooted in a commitment to decentralization, robustness, and scalability. The decentralized nature of CRDTs aligns perfectly with Drey's vision for a decentralized actuarial operating system. By enabling concurrent and independent updates without the need for a central authority, CRDTs ensure that the system remains functional and consistent, even in the face of network partitions or latency. Similarly, Nostr events provide a robust and scalable way to handle a diverse range of data types and tasks across the network.

Using CRDTs and Nostr events offers a range of capabilities within the Drey Finance Actuary Client. For instance, it enables seamless collaboration among a collection of independent parties. Each party can independently draft proposals, communicate actuarial models, have private conversations, and create partially signed Bitcoin transactions. Despite the lack of a central authority, these activities are coordinated and synchronized across the network, ensuring that all parties have a consistent view of the system state.

Another key capability enabled by this architecture is the robust handling of conflicts. In a multi-user environment, it's common for conflicting updates to occur. For example, two parties might simultaneously create a proposal or modify an actuarial model. However, thanks to the conflict-resolution properties of CRDTs, these conflicts are automatically resolved without the need for manual intervention or centralized control. This ensures the smooth operation of the system, even in highly active and dynamic environments.

In summary, the use of CRDTs and Nostr events in the Drey Finance Actuary Client is a powerful approach for building a decentralized, robust, and scalable actuarial operating system. By enabling seamless collaboration, robust conflict resolution, and the handling of a diverse range of data types and tasks, this architecture is well-suited to the needs and demands of a blockchain-powered income platform for the 21st century.

## Collaboration to Finality

The [Drey Finance Voting protocol](Operations.md#voting) serves as a bridge between the collaborative environment enabled by Nostr and CRDTs and the immutable ledger provided by the Bitcoin blockchain. For example, Drey Actuaries might need to discuss an upgrade to a mortality table. Initially, the discussion would take place within the Drey Finance Actuary Client, utilizing Nostr's event-based communication to facilitate real-time interaction and deliberation. The proposed upgrade to the mortality table would be represented as a unique data type within the CRDT framework, allowing it to be shared, scrutinized, and modified collaboratively.

Once the Actuaries are satisfied with the proposed changes, they can use the Actuary Client to create a partially signed Bitcoin transaction. This transaction represents a formal vote on the proposal and is prepared using the Ordinal-Inscription feature of the Drey Finance platform. Ordinal-Inscription is a process in which data, such as a proposed mortality table upgrade, is embedded into a Bitcoin transaction through the use of Taproot-type transactions. This mechanism allows for important information to be stored on Bitcoin's blockchain in a secure, tamper-proof manner.

The voting process itself is facilitated by the ROAST protocol's Schnorr threshold signature algorithm. Each Drey Actuary holds a share of the signature, and a certain number of these shares - the threshold - are required to validate the transaction. Once the threshold is met, the Bitcoin transaction is finalized, effectively casting the vote. This mechanism ensures the voting process is both democratic and secure, requiring a majority consensus among the Drey Actuaries.

With the vote cast, the result is then permanently stored on the Bitcoin blockchain. This represents the final step in the seamless transition from a collaborative, mutable workspace to a secure, immutable record of consensus. The newly-updated mortality table, now validated by the Actuaries' vote, becomes an unalterable part of the blockchain.

In this way, the Drey Finance Actuary Client successfully integrates the flexible, collaborative environment provided by Nostr and CRDTs with the security and permanence of the Bitcoin blockchain. This unique architecture empowers Drey Actuaries to effectively collaborate, deliberate, and reach consensus on key decisions, all while ensuring the results of their efforts are securely recorded for posterity, transparency and trust. The result is a blockchain-powered income platform that is as innovative as it is reliable, redefining retirement planning for the digital age.

## References

Martin Kleppmann, Adam Wiggins, Peter van Hardenberg, and Mark McGranaghan. Local-first software: you own your data, in spite of the cloud. 2019 ACM SIGPLAN International Symposium on New Ideas, New Paradigms, and Reflections on Programming and Software (Onward!), October 2019, pages 154–178. [doi:10.1145/3359591.3359737](https://doi.org/10.1145/3359591.3359737)

Victor B. F. Gomes, Martin Kleppmann, Dominic P. Mulligan, and Alastair R. Beresford. 2017. Verifying strong eventual consistency in distributed systems. Proc. ACM Program. Lang. 1, OOPSLA, Article 109 (October 2017), 28 pages. https://doi.org/10.1145/3133933

