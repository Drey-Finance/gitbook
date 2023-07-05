---
description: >-
  Describing the various cryptographic and communications protocols underpinning
  the Drey Network.
---

# Cryptography & Communications

## Cryptography and Communications

[Drey Actuaries software clients](architecture-iii.md#drey-actuary-client) and services utilize different cryptographic technology and communications protocols together to create robust methods for securing the network, validating and processing proof of life claims and all actuarial operations, including voting, wallet operations and distribution calculations. High level descriptions of these cryptographic and communications protocols are described below.

## Zero-Knowledge Proofs <a href="#nostr-protocol" id="nostr-protocol"></a>

A zero-knowledge proof is a cryptographic method by which one party (the prover) can prove to another party (the verifier) that they know a value x, without conveying any information apart from the fact that they know the value x.

Here's a more technical explanation:

1. **Completeness**: If the statement is true, the honest verifier (that is, one following the protocol properly) will be convinced of this fact by an honest prover.
2. **Soundness**: If the statement is false, no cheating prover can convince the honest verifier that it is true, except with some small probability.
3. **Zero-knowledge**: If the statement is true, no verifier learns anything other than this fact. This is formalized by showing that every verifier has some simulator that, given only the statement to be proved (and no access to the prover), can produce a transcript that "looks like" an interaction between the honest prover and the verifier in question.

In the context of blockchain technology, ZKPs have found a wide range of uses. For example, they are used to maintain the integrity of the transaction history while preserving the privacy of the parties involved. In Zcash, a cryptocurrency that uses a specific type of ZKP called zk-SNARKs (Zero-Knowledge Succinct Non-Interactive Argument of Knowledge), transactions are validated under the condition that no double-spending occurs, but the amount, sender, and recipient of a transaction remain private.

ZKPs are a powerful tool in the realm of blockchain and cryptography, enabling a new level of privacy and security in decentralized systems. They are an active area of research and their potential applications extend beyond blockchain into many areas of computer science and digital security.

Drey Finance uses zero-knowledge proofs to verify information in two main areas:

1. **Identity**: Users can prove, in zero knowledge, that they possess a key issued to a certain anonymized identity encapsulating identity traits without revealing the key or the identity.
2. **Computation**: A fleet of decentralized nodes can verify in zero knowledge that a particular piece of software was run correctly and that its result is a true representation of the intent of the software. This proof can be verified extremely quickly even if the underlying computation takes a very long time to run.

## Recursive Inscriptions

While neither a cryptographic or communications protocol, recursive inscriptions are important to Drey Finance's architecture. Developers have introduced the idea of calling data from existing inscriptions and using that data within new inscriptions, a concept known as a 'recursive inscription'. This could potentially allow robust software to run entirely on-chain.

Recursive inscriptions work like interconnected puzzle pieces, allowing inscriptions to borrow and use data from one another. Instead of each inscription standing alone in isolation as they always have done, they can now reference content from other inscriptions. This approach offers greater flexibility and optimizes storage efficiency. Programs can simply call already-existing repositories of inscriptions that already have complex code or data.&#x20;

Using this technique it is well within reach to create new types of permissionless smart-contracts that are enforced by Bitcoin’s indomitable hashrate and permanent storage — without requiring new cryptography.&#x20;

1. **Recursive Inscriptions**: Recursive inscriptions allow for the creation of a complex network of interconnected data sources on the Bitcoin blockchain. This can be used to store and reference large amounts of data efficiently, which is crucial for the execution of complex smart contracts.
2. **Zero-Knowledge Proofs of Correct Computation**: Zero-knowledge proofs can be used to verify the correctness of computations without revealing any information about the computation itself. This means that a smart contract's execution can be verified without revealing any sensitive information about the parties involved or the specifics of the contract.
3. **Trustless Off-Chain Smart Contracts**: By combining these two technologies, it's theoretically possible to create trustless off-chain smart contracts on the Bitcoin network. Here's how:
   * A smart contract is created and stored as a recursive inscription on the Bitcoin blockchain. This contract includes all the necessary logic and conditions for its execution.
   * When the conditions for the contract's execution are met, the contract is executed off-chain. This is performed by a fleet of [Drey's decentralized Actuary Clients](architecture-i.md#actuarial-operating-system).
   * The result of the contract's execution is then inscribed back onto the Bitcoin blockchain. This inscription includes a zero-knowledge proof of correct computation, which allows anyone to verify that the contract was executed correctly without revealing any information about the execution itself.
   * Other parties can then verify the correctness of the contract's execution by checking the zero-knowledge proof. If the proof is valid, they can be sure that the contract was executed correctly, even though the execution happened off-chain. It's also possible to daisy-chain automations this way.

This approach allows for the creation of complex, scalable, and privacy-preserving smart contracts on the Bitcoin network.

## Nostr Protocol <a href="#nostr-protocol" id="nostr-protocol"></a>

Drey Actuaries coordinate operations over the [Nostr protocol](https://nostr.com/), with each Drey Actuary running their own private client and [relay](https://nostr.com/relays). Nostr was selected because of the client / relay architecture and eventual private [asynchronous communication](https://bitcoinmagazine.com/technical/how-nostr-can-improve-bitcoin-privacy). Drey Actuaries operating their own private relays can tune their relays to accept messages from other Drey Actuaries as the medium for conducting communications for actuary operations, co-ordination on voting, cryptographic threshold signature and verifiable random function protocols, as well as in future accepting communications from other clients that Drey Actuaries may offer services to that are not yet in view. Importantly, Nostr offers a way for Proof of Life Apps to authenticate to, verify liveliness to, and receive information from Drey Actuaries in a decentralized, secure and reliable manner.

## ROAST Protocol <a href="#roast-protocol" id="roast-protocol"></a>

Drey Actuaries will undertake operations to act Schnorr signature co-signers using the [ROAST](https://eprint.iacr.org/2022/550) variant of the [FROST](https://eprint.iacr.org/2020/852) signature scheme. FROST ([Flexible Round Optimized Schnorr Threshold](https://eprint.iacr.org/2020/852.pdf)) is a powerful new kind of multisig that aggregates the key shares of federation members into a joint FROST key. To spend under this key, a threshold number of members must each produce a signature share. The shares are then combined to form a single signature that is valid under the joint FROST key. Members coordinate off chain over the nostr protocol. FROST transactions are indistinguishable from regular single-party Taproot spends. ROAST is a wrapper on top of FROST. From the research paper, "ROAST is a simple wrapper that turns a given threshold signature scheme into a scheme with a robust and asynchronous signing protocol, as long as the underlying signing protocol is semi-interactive (i.e., has one preprocessing round and one actual signing round), provides identifiable aborts, and is unforgeable under concurrent signing sessions. When applied to the state-of-the-art Schnorr threshold signature scheme FROST, which fulfils these requirements, we obtain a simple, efficient, and highly practical Schnorr threshold signature scheme."

Drey utilizes the nostr protocol to structure communications for the ROAST protocol's wrapper protocol that runs 𝑡 FROST sessions concurrently, one session for each subset of 𝑡 signers.

## Distributed Trust Authority <a href="#distributed-trust-authority" id="distributed-trust-authority"></a>

Drey Actuaries will act as [Distributed Trust Authorities](https://milagro.apache.org/docs/milagro-design), acting on requests from the Drey Proof of Life app to issue shares of a [Type-3 identity based private key](https://milagro.apache.org/docs/milagro-crypto) (for zkp identity) to anonymized identities enrolling in the fund.&#x20;

Drey Actuaries respond to a cryptographically secured request from the Drey Proof of Life App to generate a share of this identity based private key and encrypt it with a public key generated in the Drey Proof of Life App operated by the Drey Investor. The public key encryption is necessary to secure the share so that no party, including any intermediary relay, can obtain access to the share. Drey Actuaries will also provide shares of a server secret to each other Drey Actuary so individually each will be enabled to run the [M-Pin zero-knowledge proof multi-factor identity verification protocol ](https://milagro.apache.org/docs/milagro-protocols)with the Drey Investors during the Proof of Life operation every month. Note the Drey Actuaries do not need to co-ordinate with each other to issue shares, a DTA simply responds to the request from the Drey Proof of Life App or other Drey Actuaries for a share.

## **M-Pin Protocol**

M-Pin is a multi-factor authentication protocol developed by [Apache Milagro](https://milagro.apache.org/docs/milagro-intro) that provides strong security and user privacy while minimizing reliance on traditional password-based systems. It leverages pairing-based cryptography and the Distributed Trust Authority (DTA) concept to achieve its goals.

1. Secure: M-Pin is designed to provide secure user authentication without relying on passwords, which are often vulnerable to attacks, such as phishing, credential stuffing, or brute-force. Instead, it uses cryptographic keys and tokens to authenticate users, providing better security and privacy.
2. Multi-factor Authentication: M-Pin allows for multi-factor authentication (MFA), requiring users to present multiple pieces of evidence (factors) to prove their identity. These factors can include something the user knows (e.g., a PIN), something the user has (e.g., a cryptographic token), and something the user is (e.g., biometrics). This increases security by making it more challenging for an attacker to impersonate a legitimate user.
3. Pairing-Based Cryptography: M-Pin utilizes pairing-based cryptography to enable secure and efficient cryptographic operations. This allows for the construction of cryptographic primitives, such as zero-knowledge proofs, which provide strong security guarantees without revealing sensitive user information.
4. Distributed Trust Authority: M-Pin leverages Apache Milagro's DTA to decentralize trust and improve security. By distributing the responsibility of signing and validating cryptographic keys among multiple independent nodes (Decentralized Trust Authorities, or DTAs), the system becomes more resilient against attacks and failures.
5. Privacy: M-Pin ensures user privacy through zero-knowledge proof techniques, which allow users to prove their identity without revealing sensitive identifying information. In addition, the DTA model helps protect user privacy by preventing any single entity from having full control over the system.
6. Use Cases: M-Pin can be employed in various applications requiring secure user authentication, such as online services, financial transactions, and access control systems.

## Distributed Verifiable Random Function

Drey Actuaries will co-ordinate over nostr a _Distributed Verifiable Random Function_ which is a particular case of [secure multiparty computation](https://en.wikipedia.org/wiki/Secure\_multi-party\_computation) that allows a set of mutually distrustful servers to initialize and compute a [Verifiable Random Function](https://tools.ietf.org/html/draft-irtf-cfrg-vrf-05) _fsk(x)_ for strings _x_, with no trusted central party. A Verifiable Random Function can be seen as the public-key cryptography version of a keyed cryptographic hash. A prominent application for such protocols is in PoS-based consensus in distributed ledgers which require a reliable, unpredictable and unbiased source of entropy or [Decentralized](https://blog.cloudflare.com/league-of-entropy/) [Random Beacon](https://csrc.nist.gov/projects/interoperable-randomness-beacons) (DRB) to select block producers.

This DVRF protocol will enable Drey Actuaries to randomly and securely select the Drey Miner who will propose monthly distribution schedules and payouts.

