---
description: Drey's decentralised actuarial operating system explained.
---

# Architecture Overview

## Bitcoin's Universal Ledger

The advent of Taproot-type transactions has ushered in a new era for the Bitcoin Blockchain, fundamentally transforming its capabilities. Previously, the Bitcoin network was primarily used as a decentralized digital currency, with its data format being somewhat limited. However, with Taproot-type transactions, it is now possible to embed any type of data into the Bitcoin Blockchain. This means that the Bitcoin network can now serve as a universal ledger, capable of storing a wide variety of data types, not just transactional information. This opens up a plethora of new possibilities for developers and users alike, extending the utility of the Bitcoin network beyond its original purpose.

Once data is embedded into the Bitcoin Blockchain via a Taproot-type transaction, it becomes a permanent fixture on the network. This permanence is a key feature of the Bitcoin network, ensuring that once data is added to the blockchain, it cannot be altered or removed. This immutability provides a robust level of security and trust, as users can be confident that the data they see on the blockchain is accurate and has not been tampered with. This feature is particularly valuable in applications where data integrity is paramount, such as in legal contracts, property deeds, academic records, and actuarial operations.

In addition to permanence, data embedded into the Bitcoin Blockchain via Taproot-type transactions also inherits other key features of the Bitcoin network, such as availability and determinism. Availability ensures that the data is always accessible to anyone on the network, regardless of their geographical location or the time of day. This global accessibility is a cornerstone of the decentralized nature of the Bitcoin network. Determinism, on the other hand, ensures that the outcome of any transaction is predictable and consistent, regardless of when or where it is executed. This feature is crucial for the reliable operation of smart contracts and other automated processes on the blockchain. Together, these features make the Bitcoin network a powerful platform for a wide range of applications, far beyond its original use as a digital currency.

As described in following sections, Drey Finance leverages Bitcoin as a universal ledger, storing actuarial models, payout schedules, source code, proposals and vote records and more inside the Bitcoin blockchain. Bitcoin's features of data permanence, accessibility and determinism are unmatched by other distributed storage models available. By undertaking the goal of decentralizing actuarial operations, Drey Finance itself is held to a higher standards where longevity of data immutability, durability and accessibility will be measured across lifetimes. We believe Bitcoin as a universal ledger enables this vision to become reality.

## Architecture

### Overview

Drey Finance consists of two major components. First, there is a Proof of Life app for iOS and Android whose main function is to verify the liveliness of the Drey Fund investor so that they can receive their monthly annuity payment. In addition, the app enables a fund investor to get up to the second accurate information on payout, yield income generated, opt-in co-ordination for those wishing to be Sharia compliant, and other operations.&#x20;

Second, the Drey Decentralized Actuary Network is a federation consisting of independent parties co-ordinating over the Nostr client/relay network to action actuarial processes and wallet operations for the benefit of the Drey Fund investors.

<figure><img src=".gitbook/assets/Drey Finance - Diagram 2.png" alt=""><figcaption><p>Figure 1. Drey Finance Architecture Overview</p></figcaption></figure>

### Proof of Life App

Drey's Proof of Life app delivers more functionality that just verifying the liveliness of customer. It is the primary method of interacting with the Drey Finance decentralized actuarial operating system. The Proof of Life App's main functions include the following:

* Demographic Verification
* Proof of Life Verification
* Account Settings & Information
* Fiat on-ramp / off-ramp

#### Demographic Verification

The app verifies the age, sex and geography of Drey Fund investors during enrolment. This information is obtained via third party identity and KYC service providers contracted to Drey Finance. The user experience will be akin to signing up to any centralised exchange or finance institution, and should be less painful, as the amount of information necessary to obtain and verify is small:

* Age
* Birth Month and Year
* Citizenship
* Country of Residence

Note that name, address or any other personally identifying information IS NOT required to be stored on an ongoing basis, and none is. Instead, a content-based GUID ([RFC 4122](http://www.ietf.org/rfc/rfc4122.txt) describes the conventions) is created from the obtained information and this applies as the unique identifier for the Drey Fund investor. Drey Actuaries are never party to, and will never know, any personally identifying information of a Drey Fund investor.

The Drey Proof of Life App is configured to comply with U.S. State Department terrorism watch list and EU sanctions list, so any identities from these geographies (North Korea, Iran, Syria, etc.) are not eligible to create Drey Fund accounts and will not be serviced.

#### Proof of Life Verification

Drey utilizes zero knowledge proof technology to authenticate a user to the Drey Actuary network without revealing any personally identifying details. As described in [following sections](cryptography-overview.md), zero-knowledge proof technology is a cryptographic method that allows one party (the prover) to prove to another party (the verifier) that they know a specific piece of information without revealing that information itself. This technology is particularly useful for authentication processes where the goal is to verify an identity without revealing any personally identifiable information.

In the context of the technology used in Drey Finance, the zero-knowledge proof technology works by using a multi-factor authentication protocol built upon zero-knowledge proofs. When a user wants to authenticate themselves, they create a proof that shows they know how to re-create their secret information (like a password or a private key) from something they have (a device), something they know (a pin) and something they are (a biometric) without actually revealing that secret information. This proof is then sent to the verifier.

The verifier, having the public information corresponding to the user's secret, can verify the proof without learning anything about the user's secret. This is the "zero-knowledge" aspect of the protocol. If the proof is valid, the verifier can be sure that the user knows their secret, and thus the user's identity is authenticated.

This process removes the need for a traditional Public Key Infrastructure (PKI) system, where certificates are issued to bind a public/private key pair to an identity. Instead, the identity management and key lifecycle can take place within the decentralized actuarial operating system itself.

In certain use cases, this technology can make systems easier to scale and manage than traditional PKI, eliminate root key 'single point of compromise' weaknesses, and provide a seamless fit for today's decentralized networks and distributed systems.

After the initial enrolment workflow is completed for identity verification, each month, when the customer's Drey distribution is ready to obtained, the customer simply opens their Drey app, authenticates with FaceID, inputs a six digit pin, and the process of Proof of Life is complete. The experience is seamless and frictionless. Once authenticated into the app the Drey customer can obtain principal balances, opt-in/out of yield generation programs, view expected portfolio returns,   and/or select fiat off-ramps for their distributions, among other actions.

#### Account Settings and Information

The Proof of Life app will also enable users to configure their settings for:

* Alerts, notifications&#x20;
* Opt-in to yield generation programs, or stay opt-out in order to remain [Sharia compliant](https://www.bankofengland.co.uk/explainers/what-is-islamic-finance)
* Fiat-off ramps
* Setup additional accounts (for couples or children)

#### Fiat on-ramps/off-ramps

The Drey Proof of Life app also enables distributions to be automatically converted to fiat, with distributions directed to Drey Finance's exchange partners over the [lightning network](https://lightning.network/). Drey Finance will negotiate the best exchange rate by volume with partners on behalf of the Drey customer, and utilize the lightning network to make instant payments to the exchange partner.&#x20;

The app will enable the user to setup their own remittance information with the exchange partner's database through an integration into their API. It is envisioned that a number of exchange partners will be utilized and enabled based on geography and regulatory requirements.

This same infrastructure will be utilized for fiat on-ramps. The Drey Proof of Life app will enable, post identity verification and enrolment, a user to utilize bank accounts and/or debit cards to fund their account to the best extent possible for that user's given geography and jurisdiction. The app's emphasis on user experience and design for on-boarding (and use of AI) will prompt the user the best/easiest way to fund their account as a main design objective.

### Drey Actuary Network

