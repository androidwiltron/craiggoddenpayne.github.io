---
layout: post
title: Blockchain - Part 1
image: /assets/img/2018-2-16-blockchain/blockchain.jpg
tags: blockchain dlt
---

![blockchain](/assets/img/2018-2-16-blockchain/blockchain.jpg)
I've recently been taking a course on blockchain, as it's something that I find quite interesting. Blockchains have recently gained popularity in several industries, and although I am yet to use them in my day to day, it's something I can definitely see comin in the near term.

Blockchains can solve problems and create efficiencies in tech areas such as privacy, security and data sharing. Blockchains help to move away from the centralized "one source of truth" monolith database, that most companies have. In fact in almost every job I have had, there is always a huge, single production database, that contains all the business critical data, and if it were to go down, there would be chaos.

Since as far back as I can remember, we have always been trying to move away from centralised computing, and splitting software into smaller chunks, microservices and moving into the cloud. One thing that always remains is a huge monolith database. I've seen this change slightly into smaller, domain specific databases and stores, but usually there is still a single point where everything comes together.

A blockchain is a type of distributed ledge technology, which basically means it is a data structure which resides across multiple computing devices, typically spread across multiple devices and regions. DLTs existed before bitcoin, but bitcoin brought together some of the core ideas, with regards to timestamping, P2P, crytography and sharing the computing power. A good description of a

DTL could be summed up in through points:

- Data structure that captures the current state of a ledger
- Transactions that change the ledger state
- Protocol to allow transactions to be accepted

<p align="center">
  <img src="/assets/img/2018-2-16-blockchain/p2p.jpg" alt="p2p"/>
</p>

A blockchain will track various assets transactions. The transactions are are grouped into blocks. There be any number of these transactions in a block. Nodes on the blockchain network group up the transactions and send them through the network. They are synced up by an agreement by all peers, and eventually each node will contain an up to date version of the ledger. Blockchain just basically a P2P distributed ledger, which is ruled by smart contracts. Smart contracts are just predefined actions that are performed when certain conditions are met.

Blockchain used to be referred to as the specific data structure within a DLT, but now a lot of people use the term blockchain to refer to anything, from cryptocurrencies to enterprise deployments of DLTs. Blockchain is a very wide term, and is comparable to the word internet.

Blockchain is in a basic form, a chronological chain of blocks of transactions, that are bundled together and added to the chain, at the same time.

Bitcoin is a good example to explain this in more detail:

<p align="center">
  <img src="/assets/img/2018-2-16-blockchain/bitcoin.jpg" alt="bitcoin"/>
</p>

Miner nodes bundle unconfirmed and valid transactions into a block. The miners must then solve a cryptographic challenge, to propose the next block. People refer to this as "proof of work".

A block consists of 4 metadata.
- Reference of previous block
- Proof of work (known as nonce)
- Timestamp
- Merkle tree root of transacions

to be continued...