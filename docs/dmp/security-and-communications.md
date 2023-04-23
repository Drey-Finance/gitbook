# Security and Communications

Drey Miners utilize different cryptographic technology and communications protocols together to create a robust but methods for securing the network, processing proof of life claims, issuing DREY tokens and actuary operations.&#x20;

## nostr Protocol

Drey Miners coordinate operations over the [nostr protocol](https://nostr.com/), with each Drey Miner running their own private [relay](https://nostr.com/relays). Nostr was selected because of the client / relay architecture. Drey Miners operating their own private relays can tune their relays to accept messages from other Drey Miners, as well as other clients that Drey Miners may offer services to that are not yet in view.

## ROAST Protocol

Drey Miners will undertake operations to act signers using the [ROAST](https://eprint.iacr.org/2022/550) variant of the [FROST](https://eprint.iacr.org/2020/852) signature scheme.&#x20;

From the research paper, "ROAST is a simple wrapper that turns a given threshold signature scheme into a scheme with a robust and asynchronous signing protocol, as long as the underlying signing protocol is semi-interactive (i.e., has one preprocessing round and one actual signing round), provides identifiable aborts, and is unforgeable under concurrent signing sessions. When applied to the state-of-the-art Schnorr threshold signature scheme FROST, which fulfils these requirements, we obtain a simple, efficient, and highly practical Schnorr threshold signature scheme."

Drey's intention is to utilize the nostr protocol to structure communications for the ROAST protocol's wrapper protocol that runs 𝑡 FROST sessions concurrently, one session for each subset of 𝑡 signers.

## Distributed Trust Authority

{% embed url="https://s.icepanel.io/GCDG3OFGyF6DnX/qqQl" %}
