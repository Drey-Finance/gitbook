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

Second, the Drey Decentralized Actuary Network consists of independent parties co-ordinating over the Nostr client/relay network to action actuarial processes and wallet operations for the benefit of the Drey Fund investors.

<figure><img src=".gitbook/assets/Drey Finance - Diagram 1.png" alt=""><figcaption><p>Figure 1. Drey Architecture</p></figcaption></figure>

### Proof of Life App

The Proof of Life App's main functions include the following:

* Demographic Verification
* Proof of Life Verification
* Account Information
* Accounts Settings

#### Demographic Verification

The app verifies the age, sex and geography of Drey Fund investors during enrolment. This information is obtained via third party identity and KYC service providers contracted to Drey Finance. The user experience will be akin to signing up to any centralised exchange or finance institution, and should be less painful, as the amount of information necessary to obtain and verify is small:

* Age
* Birth Month and Year
* Citizenship
* Country of Residence

Note that name, address or any other personally identifying information IS NOT required to be stored on an ongoing basis, and none is. Instead, a content-based GUID ([RFC 4122](http://www.ietf.org/rfc/rfc4122.txt) describes the conventions) is created from the obtained information and this applies as the unique identifier for the Drey Fund investor. Drey Actuaries are never party to, and will never know, any personally identifying information of a Drey Fund investor.

The Drey Proof of Life App is configured to comply with U.S. State Department terrorism watch list and EU sanctions list, so any identities from these geographies (North Korea, Iran, Syria, etc.) are not eligible to create Drey Fund accounts and will not be serviced.

#### Proof of Life Verification

Drey utilizes zero knowledge proof technology to authenticate a user to the Drey Actuary network without revealing any personally identifying details. As described in [following sections](cryptography-overview.md),&#x20;
