---
description: Drey's decentralised actuarial operating system explained.
---

# Architecture III

## CRDTs

CRDTs, or Conflict-Free Replicated Data Types, are a class of data structures that are uniquely designed for multi-user applications. They were introduced in 2011 in academic computer science research. Like standard data structures such as hash maps and lists, CRDTs can store document state, but with the added feature of handling multi-user interactions right from the ground up. They are designed to tolerate concurrent updates from different users and to resolve conflicting updates without requiring any central authority or consensus mechanism. Essentially, CRDTs allow multiple replicas of the same data to be updated independently and concurrently, and yet eventually converge to a consistent state.

In the context of the Drey Finance Actuary Client, CRDTs are used to store, manage and communicate different types of data across the network. One of the key applications is implementing Nostr events as different data types. Nostr is a protocol designed for creating and handling shared events across a network, and it's a perfect match for the decentralized nature of Drey's actuarial operations. Nostr events can represent a variety of data types, such as proposals, actuarial models, private conversations, and partially signed bitcoin transactions. Each of these data types corresponds to a specific action or task performed by the actuarial operating system, and using Nostr events allows these tasks to be communicated and processed in a decentralized way.

The choice to use CRDTs and Nostr events within the Drey Finance Actuary Client is rooted in a commitment to decentralization, robustness, and scalability. The decentralized nature of CRDTs aligns perfectly with Drey's vision for a decentralized actuarial operating system. By enabling concurrent and independent updates without the need for a central authority, CRDTs ensure that the system remains functional and consistent, even in the face of network partitions or latency. Similarly, Nostr events provide a robust and scalable way to handle a diverse range of data types and tasks across the network.

Using CRDTs and Nostr events offers a range of capabilities within the Drey Finance Actuary Client. For instance, it enables seamless collaboration among a collection of independent parties. Each party can independently draft proposals, communicate actuarial models, have private conversations, and create partially signed Bitcoin transactions. Despite the lack of a central authority, these activities are coordinated and synchronized across the network, ensuring that all parties have a consistent view of the system state.

Another key capability enabled by this architecture is the robust handling of conflicts. In a multi-user environment, it's common for conflicting updates to occur. For example, two parties might simultaneously create a proposal or modify an actuarial model. However, thanks to the conflict-resolution properties of CRDTs, these conflicts are automatically resolved without the need for manual intervention or centralized control. This ensures the smooth operation of the system, even in highly active and dynamic environments.

In summary, the use of CRDTs and Nostr events in the Drey Finance Actuary Client is a powerful approach for building a decentralized, robust, and scalable actuarial operating system. By enabling seamless collaboration, robust conflict resolution, and the handling of a diverse range of data types and tasks, this architecture is well-suited to the needs and demands of a blockchain-powered income platform for the 21st century.
