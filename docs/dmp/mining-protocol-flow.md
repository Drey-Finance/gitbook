# Mining Protocol Flow

## On-boarding

Each new investor in Drey will be given a P2TR MultiSig with HTLC wallet address under control of the Drey mining pool. This is not the Drey Vault but an interim on-boarding wallet address that requires a super majority (67%) to sign the transaction else it will be returned to the user. This is a stop gap measure to insure the Drey Proof of Life/KYC service approves the transaction as well, providing safeguards that non-KYCd funds do not contaminate the Drey Vault containing the bitcoin.

If the transaction is agreed to by the Drey Miners and KYCd service the funds, once confirmed in the on-boarding wallet, will be swept into the Drey BTC Vault. This wallet is a FROST enabled P2TR address under control of the miners solely.

