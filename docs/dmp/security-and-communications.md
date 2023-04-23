# Security and Communications

Drey Miners utilize different cryptographic technology and communications protocols together to create a robust but methods for securing the network, processing proof of life claims, issuing DREY tokens and actuary operations (including voting).&#x20;

## nostr Protocol

Drey Miners coordinate operations over the [nostr protocol](https://nostr.com/), with each Drey Miner running their own private [relay](https://nostr.com/relays). Nostr was selected because of the client / relay architecture. Drey Miners operating their own private relays can tune their relays to accept messages from other Drey Miners as the medium for conducting communications for actuary operations, co-ordination on voting, cryptographic threshold signature and verifiable random function protocols, as well as in future accepting communications from other clients that Drey Miners may offer services to that are not yet in view.

## ROAST Protocol

Drey Miners will undertake operations to act signers using the [ROAST](https://eprint.iacr.org/2022/550) variant of the [FROST](https://eprint.iacr.org/2020/852) signature scheme.&#x20;

From the research paper, "ROAST is a simple wrapper that turns a given threshold signature scheme into a scheme with a robust and asynchronous signing protocol, as long as the underlying signing protocol is semi-interactive (i.e., has one preprocessing round and one actual signing round), provides identifiable aborts, and is unforgeable under concurrent signing sessions. When applied to the state-of-the-art Schnorr threshold signature scheme FROST, which fulfils these requirements, we obtain a simple, efficient, and highly practical Schnorr threshold signature scheme."

Drey's intention is to utilize the nostr protocol to structure communications for the ROAST protocol's wrapper protocol that runs 𝑡 FROST sessions concurrently, one session for each subset of 𝑡 signers.

## Distributed Trust Authority

Drey Miners will act as [Distributed Trust Authorities](https://milagro.apache.org/docs/milagro-design), acting on requests from the Drey Proof of Life service to issue shares of a [Type-3 identity based private key](https://milagro.apache.org/docs/milagro-crypto) to randomised identities enrolling in the fund.&#x20;

See the figure below for Level 1 C4 diagram of the services in play.

{% embed url="https://s.icepanel.io/GCDG3OFGyF6DnX/qqQl" %}

Drey Miners respond to a cryptographically secured request from the Drey Proof of Life Service (operated by Drey Finance) to generate a share of this identity based private key and encrypt it with a public key generated in the Drey Proof of Life App operated by the Drey Investor. The public key encryption is necessary to secure the share so that no party, including the Drey Proof of Life App, can obtain access to the share.

Drey Miners will also provide shares of a server secret to the Drey Proof of Life Service so that it can run the [M-Pin zero-knowledge proof multi-factor identity verification protocol ](https://milagro.apache.org/docs/milagro-protocols)with the Drey Investors during the Proof of Life operation every month.

### About M-Pin

M-Pin is a multi-factor authentication protocol developed by [Apache Milagro](https://milagro.apache.org/docs/milagro-intro) that provides strong security and user privacy while minimizing reliance on traditional password-based systems. It leverages pairing-based cryptography and the Distributed Trust Authority (DTA) concept to achieve its goals.

Executive Summary:

1. Purpose: M-Pin is designed to provide secure user authentication without relying on passwords, which are often vulnerable to attacks, such as phishing, credential stuffing, or brute-force. Instead, it uses cryptographic keys and tokens to authenticate users, providing better security and privacy.
2. Multi-factor Authentication: M-Pin allows for multi-factor authentication (MFA), requiring users to present multiple pieces of evidence (factors) to prove their identity. These factors can include something the user knows (e.g., a PIN), something the user has (e.g., a cryptographic token), and something the user is (e.g., biometrics). This increases security by making it more challenging for an attacker to impersonate a legitimate user.
3. Pairing-Based Cryptography: M-Pin utilizes pairing-based cryptography to enable secure and efficient cryptographic operations. This allows for the construction of cryptographic primitives, such as zero-knowledge proofs, which provide strong security guarantees without revealing sensitive user information.
4. Distributed Trust Authority: M-Pin leverages Apache Milagro's DTA to decentralize trust and improve security. By distributing the responsibility of signing and validating cryptographic keys among multiple independent nodes (Decentralized Trust Authorities, or DTAs), the system becomes more resilient against attacks and failures.
5. Privacy: M-Pin ensures user privacy through zero-knowledge proof techniques, which allow users to prove their identity without revealing sensitive information. In addition, the DTA model helps protect user privacy by preventing any single entity from having full control over the system.
6. Use Cases: M-Pin can be employed in various applications requiring secure user authentication, such as online services, financial transactions, and access control systems.

The M-Pin protocol from Apache Milagro provides a robust and secure alternative to traditional password-based authentication systems. By utilizing pairing-based cryptography, multi-factor authentication, and a decentralized trust model, M-Pin offers increased security and privacy for users and service providers alike
