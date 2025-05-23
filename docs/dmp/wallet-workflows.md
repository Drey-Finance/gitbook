---
description: Steps describing wallet workflows and cryptographic requirements
---

# Wallet Workflows

This document attempts to lay out the wallet workflows between entities, list the cryptographic underpinning of each wallet (for example, P2TR/Schnorr) and point out where ideal wallet operations are not supported by the cryptographic capabilities of the decentralised mining pool. The decentralised mining pool only support P2TR transactions (as currently spec'd) and the underlying Stacks protocol only supports ECDSA, although verification of Schnoor signatures is planned for a future release.

This exercise is necessary because not all wallets support P2TR wallet adresses. So moving funds into a P2TR address may necessitate the existence of an on-boarding wallet undr.



There are two ways a user can deposit bitcoin into the Drey Vault.&#x20;

1. A user contracts with the Proof of Life Service to buy bitcoin, and the bitcoin is moved directly into the Drey Vault by the Proof of Life Service. This does not require the necessity of an on-boarding wallet described below as the user will have already been KYC'd by the Proof of Life service.
2. A user can make their own deposit of bitcoin into the Drey Vault &#x20;
