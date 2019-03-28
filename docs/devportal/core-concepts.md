# Core Concepts

Blockchains have many facets, Komodo more than most.  This section aims to start creating an understanding of foundational knowledge in working with the most advanced blockchain toolkit.

The [dApps](../dapps-crypto-conditions/dapps) section is made up of components available out-of-the-box. 

Summary:

* Public key cryptography is used when a private and public key pair are used for proving something.
* Private Keys are stored in a wallet, not on the blockchain <--also important
* Private keys sign transactions. <--fundamental
* Signatures on transaction are proven by the network using the corresponding public key to spend the claimed ownership of funds. <--validation, the single most important thing in this priv/public key use.
* Transactions fill blocks, like an item on a shopping list fills a piece of paper.
* Blocks are arranged in sequential order, forming a chain.
* Each block contains agreed transactional information.  The proof of the transactional detail and it's arrangement in the block is called consensus.  Consensus is achieved by each participant relying on their own computation.
* The jigsaw puzzle of finding first correct order of tx data within block wins the reward.  Coins.
* Coins & Tokens are used in transaction details to transfer value.
* Nodes is the jargon term for computers that do the computations to maintain the network.
* Some nodes are heavily computational (miners), some are quiet and store a valuable private key within it's wallet.
* There's software to make this system easier to use and useful for transfering value, like the internet for information (SPV, DEX, Explorers vs webserver, database, email, streaming protocols)


## Cryptography Overview
Cryptography is a branch of maths that is interested in maintaining secrets.  It's etymology (origin of the word) comes from Greek.  Kryptos meaning hidden/secret, grafi meaning write/study.

Applying cryptographic study (the maths) into science and engineering leads us to the discovery of encryption.  We rely on being able to prove knowledge of a secret, without revealing the secret.  This is fundamental to the trustless peer to peer blockchain network.

Cryptography is used to control blockchain artifacts (coins, assets, gameplay, objects) by using keys, wallets and addresses.

## Signature & Signature Scheme
Digital signatures are used to spend funds.  Without a valid signature, the claim of ownership of the underlying asset cannot be validated.  No validation (proof) equals no spend.

A key signs data resulting in a signature.  The data is transaction details.  The who, how much and what conditions of value transfer.

The signature scheme used for signing transactions is called ECDSA (elliptic curve digital signing algorithm).  The parameters used for this curve are secp256k1.  The equation for this is y^2 = x^3 + 7 (over real numbers - not the imaginary square root of minus ones).

## Wallet
The wallet is completely independent from the blockchain.  Generation and management of the wallet can be done without reference to the blockchain or the internet.  There are no coins in a wallet.

## Keys
Ownership on the blockchain is established through digital keys.  The keys are not stored on the network, they are stored on a users's device - in the "wallet".

A private key is used to sign specific transaction details.  This signature can only pass validation for the contents of this specific transaction.  It will not pass validation for any other transactions.

Keys enable the most interesting properties of a peer-to-peer network.  Trust, control, ownership, and the cryptographic security of the network rely on these keys.

## Transactions
Transactions rely on digital signatures stored in the blockchain (not the private keys).  Signatures are only generated with a private key.  To make a valid transaction, you need to have a key and the key must own something to transact - coins.

The proof that you had ownership of the coins to spend, is in the signature portion of the transaction.  The signature releases the funds for spending in this unique transaction.

### Transaction Fees
To conduct any transactions, usually but not all the time, a fee is required.  There are ways to make fee-less transactions which will be covered in a guide.

## Blocks
This information to be merged from src repo.

## Consensus
This information to be merged from src repo.

## Coins & Tokens
This information to be merged from marketing repo.

### Proxy Token
This information to be merged from marketing repo.

## Nodes
This information to be merged from src repo.

## Address
This information to be merged from src repo.

## UTXO
This information to be merged from src repo.

## Atomic Swap
This information to be merged from marketing repo.

## Exchanges
This information to be merged from marketing repo.

### Centralized
This information to be merged from marketing repo.

### Decentralized
This information to be merged from marketing repo.