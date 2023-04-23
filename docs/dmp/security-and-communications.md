# Security and Communications

Drey Miners will undertake operations to act signers using the [ROAST](https://eprint.iacr.org/2022/550) variant of the [FROST](https://eprint.iacr.org/2020/852) signature scheme. They will co-ordinate operations over the [nostr protocol](https://nostr.com/), with each Drey Miner running their own [relay](https://nostr.com/relays).&#x20;

From the research paper, "ROAST is a simple wrapper that turns a given threshold signature scheme into a scheme with a robust and asynchronous signing protocol, as long as the underlying signing protocol is semi-interactive (i.e., has one preprocessing round and one actual signing round), provides identifiable aborts, and is unforgeable under concurrent signing sessions. When applied to the state-of-the-art Schnorr threshold signature scheme FROST, which fulfils these requirements, we obtain a simple, efficient, and highly practical Schnorr threshold signature scheme."

{% embed url="https://s.icepanel.io/GCDG3OFGyF6DnX/qqQl" %}
