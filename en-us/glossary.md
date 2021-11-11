# Glossary

## Blockchain

#### CET

`CET` is the native cryptocurrency used by the `CSC` ecosystem.

#### Account

An object containing an address, balance, nonce and optional storage and code. An account can be a contract account or an EOA (externally owned account).

#### EOA

Externally Owned Account. An account with public and private keys created by an external user.

#### Contract Account

An account containing code that executes whenever it receives a transaction from another account (EOA or contract).

#### Address

Most generally, this represents an EOA or contract that can receive (destination address) or send (source address) transactions on the blockchain. More specifically, it is the right-most 160 bits of a Keccak hash of an ECDSA public key.

#### Nonce

In cryptography, a value that can only be used once. Each account has a Nonce, which acts as a transaction counter to prevent replay attacks.

#### Network

Referring to the `CSC` network, a peer-to-peer network that propagates transactions and blocks to every `CSC` node.

#### Testnet

`CSC` test network. Short for "test network".

#### Faucet

A service that dispenses testnet `CET` for free testing on a testnet.

#### Node

A software client that participates in the network.

#### Consensus

The block validation rules that full nodes follow to stay in consensus with other nodes. 

#### Proof-of-Stake (PoS) Consensus

Proof-of-Stake is a distributed consensus mechanism used by `CSC`. Proof-of-Stake consensus asks users to prove ownership of a certain amount of cryptocurrency (their "stake" in the network) in order to be able to participate in the validation of transactions.

#### Validator

A participant in `CSC` network, responsible for verifying transactions and generating blocks. Validators need to submit a security deposit(stake) in order to get included in the validator set.

#### Reward

The total transaction fee in each new block plus a fixed block reward is the reward of the network to validators.

#### Block

A block is a package of data that contains zero or more transactions, the hash of the previous block (“parent”), and optionally other data. 

#### Genesis Block

The first block in a blockchain, used to initialize a particular network.

#### Blockchain

A sequence of blocks validated by the consensus rule. Because each block (except for the initial “genesis block”) points to the previous block, the data structure that they form is called a “blockchain”.

#### Fork

This term assumes two main meanings: a change in protocol that leads to a fork in the chain, or a temporal divergence in two potential block paths during the block generation process.

#### Hard Fork

A hard fork is a permanent divergence in the blockchain. one commonly occurs when non-upgraded nodes can’t validate blocks created by upgraded nodes that follow newer consensus rules. 

#### Difficulty

A field in the block header that indicates whether the block is generated sequentially.

#### Transaction

Data committed to the blockchain signed by an originating account, targeting a specific address. The transaction contains metadata such as the gas limit for the transaction.

#### Gas

A virtual fuel used in `CSC` to execute smart contracts. The Ethereum Virtual Machine uses an accounting mechanism to measure the consumption of gas and limit the consumption of computing resources.

#### Gas Limit

The maximum amount of gas a transaction or block may consume.

#### Gas Used

The amount of gas actually consumed by a transaction or block.

#### Gas Price

The price of gas of a transaction.

#### Gas Fee

The gas price of a transaction multiplied by the gas used is equal to the gas fee.

#### Contract Creation Transaction

A special transaction, with the "zero address" as the destination address, that is used to create a contract on `CSC`.

#### Transaction Pool

The transaction pool refers to the collection of pending transactions that have been created by users and are pending confirmation by validators in a node.

#### Receipt

Data returned by an `CSC` client to represent the result of a particular transaction, including a hash of the transaction, its block number, the amount of gas used and, in case of deployment of a Smart Contract, the address of the Contract.

#### Internal Transaction

A transaction sent from a contract account to another contract account or an EOA.

#### Wei

The smallest denomination of `CET`. 10^18 `Wei` = 1 `CET`.

#### Zero Address

A special address, composed entirely of zeros, that is specified as the destination address of a contract creation transaction.

#### Merkle Patricia Tree

A data structure used in `CSC` to efficiently store key-value pairs.

## Smart Contract

#### Smart Contract

A piece of code deployed on the blockchain. A computer protocol meant to streamline the process of contracts by digitally enforcing, verifying, or otherwise managing them. Given the nature of the blockchain, all of these transactions are visible and verifiable through the code itself.

#### EVM

Ethereum Virtual Machine, a stack-based virtual machine which executes bytecode, for running smart contract code. 

#### Bytecode

Abstract instruction set designed for efficient execution by a software interpreter or a virtual machine. Unlike human readable source code, bytecode is expressed in numeric format.

#### EVM Assembly Language

A human-readable form of EVM bytecode.

#### Compiling

Converting code written in a high-level programming language (e.g. Solidity) into a lower level language (e.g. EVM bytecode).

#### Library

A library is a special type of contract that has no payable functions, no fallback function, and no data storage. Therefore, it cannot receive or hold `CET`, or store data. A library serves as previously deployed code that other contracts can call for read-only computation.

#### Solidity

A procedural programming language with syntax that is similar to JavaScript, C++ or Java. The most popular and most frequently used language for smart contracts.

#### Vyper

A high-level programming language, similar to Serpent, with Python-like syntax, intended to get closer to a pure-functional language. It is also a language for smart contracts.

#### Event

An event allows the use of EVM logging facilities. DApps can listen for events and use them to trigger JavaScript callbacks in the user interface. For more information, see http://solidity.readthedocs.io/en/develop/contracts.html#events .

#### Assert

In Solidity, `assert(false)` compiles to `0xfe`, an invalid opcode, which uses up all remaining gas and reverts all changes. When an `assert()` statement fails, something very wrong and unexpected should be happening, and you will need to fix your code. You should use assert to avoid conditions which should never, ever occur.

#### Fallback Function

A default function called in the absence of data or a declared function name.

#### Immutable Deployed Code Problem

Once a contract’s (or library’s) code is deployed it becomes immutable. Standard software development practices rely on being able to fix possible bugs and add new features, so this represents a challenge for smart contract development.

#### Re-entrancy Attack

An attack that consists of an Attacker contract calling a Victim contract function in such a way that during execution the Victim calls the Attacker contract again, recursively. This can result, for example, in the theft of funds by skipping parts of the Victim contract that update balances or count withdrawal amounts.

## Cryptography

#### Hash

fixed-length fingerprint of variable-size input, produced by a hash function.

#### Keccak256

Cryptographic hash function used in `CSC`. Keccak256 was standardized as SHA-3.

#### SHA

The Secure Hash Algorithm (SHA) is a family of cryptographic hash functions published by the National Institute of Standards and Technology (NIST).

#### Digital Signature

A digital signing algorithm is a process by which a user can produce a short string of data called a "signature" of a document using a private key such that anyone with the corresponding public key, the signature, and the document can verify that (1) the document was "signed" by the owner of that particular private key, and (2) the document was not changed after it was signed.

#### ECDSA

Elliptic Curve Digital Signature Algorithm, or ECDSA, is a cryptographic algorithm used by `CSC` to ensure that funds can only be spent by their owners.

#### Private Key

The secret number that allows `CSC` users to prove ownership of an account or contracts, by producing a digital signature.

#### Public Key

A number, derived via a one-way function from a private key, which can be shared publicly and used by anyone to verify a digital signature made with the corresponding private key.

#### Keystore File

A JSON-encoded file that contains a single (randomly generated) private key, encrypted by a passphrase for extra security.

## Ecosystem

#### Wallet

Software to manage accounts. Used to access and control `CSC` accounts and interact with Smart Contracts. Keys need not be stored in a wallet, and can instead be retrieved from an offline storage (e.g. paper) for improved security.

#### IDE

Short for Integrated Development Environment, an integrated user interface that typically combines a code editor, compiler, runtime, and debugger.

#### Truffle

One of the most commonly used Dapp Development Frameworks.

#### Redhat

One of the most commonly used Dapp Development Frameworks.

#### Ganache

Software that can run an individual's Ethereum blockchain, for running tests, executing commands, and inspecting status.

#### Web3

The third version of the web. First proposed by Gavin Wood, Web3 represents a new vision and focus for web applications: from centrally owned and managed applications, to applications built on decentralized protocols.

#### Whisper

A decentralized (P2P) messaging service. It is used along with Web3 and Swarm to build DApps.

#### Swarm

A decentralized (P2P) storage network, used along with Web3 and Whisper to build DApps.

#### DAO

Decentralized Autonomous Organization.

#### DApp

Decentralized Application. At a minimum, it is a smart contract and a web user-interface. More broadly, a DApp is a web application that is built on top of open, decentralized, peer-to-peer infrastructure services. 

#### DEFI

Short for Decentralized Finance referring to financial smart contracts, protocols, and decentralized applications built on blockchain.

#### DEX

Decentralized Exchange.

#### NFT

A non-fungible token. This is a token standard introduced by the ERC721 proposal. NFTs can be tracked and traded, but each token is unique and distinct; they are not interchangeable like ERC20 tokens. NFTs can represent ownership of digital or physical assets.
