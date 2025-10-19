# **Ethereum: A Simplified Overview**

## **0. Network Number Calculation**
Date: **03.03.91**

We calculate the number **S = D + M + Y**:
- D = 3 (day)
- M = 3 (month)
- Y = 91 (year)

**S = 3 + 3 + 91 = 97**

Then, **R = (S mod 16) + 1**

97 mod 16 = 1 → **R = 1 + 1 = 2**

Network number **2** corresponds to **Ethereum**.  
Thus, Ethereum was selected for analysis.

---

## **1. General Information**
**Ethereum** is a public blockchain platform launched on **July 30, 2015**, created by **Vitalik Buterin** and co-founders such as **Gavin Wood**. The **first block of the main Ethereum network (the so-called genesis block)** was generated on this day, marking the official launch of the Ethereum mainnet.  
Ethereum’s main purpose is to go beyond digital payments and provide a **decentralized platform** for **smart contracts** and **decentralized applications (dApps)** — applications that run **without intermediaries**.  

The native cryptocurrency, **Ether (ETH)**, is used to:
- Pay transaction fees (*gas*);
- Power smart contract execution;
- Participate in staking and network consensus.

---

## **2. Consensus Mechanism**
### **Before 2022 — Proof of Work (PoW)**
In the PoW model, miners validated transactions by solving complex mathematical problems.  
While this ensured high security, it required **massive energy consumption**.

### **After 2022 — Proof of Stake (PoS)**
After **The Merge** on **September 15, 2022**, Ethereum switched to PoS.  
Now, blocks are created by **validators** who lock up **32 ETH** as a deposit.  

Key facts:
- Blocks are produced every **~12 seconds**;
- Energy usage dropped by **over 99%**;
- Dishonest validators are penalized (*slashing*).

---

## **3. Data Storage Structure**
Each block in the blockchain is like a **page in a ledger**, containing a **group of transactions and other data**.  
A block consists of a **header** (metadata) and a **list of transactions**.  
To store data efficiently and verify its integrity, Ethereum uses a **Merkle Patricia Trie** — a special cryptographic data structure.  

Each Ethereum block includes:
- A **header** — containing metadata and hashes;
- A **body** — containing a list of transactions.

Key fields in the header:
- `parentHash` — links to the previous block;
- `stateRoot`, `transactionsRoot`, `receiptsRoot` — cryptographic hashes summarizing state, transactions, and receipts.

---

## **4. Hash Algorithm**
Ethereum ensures **data immutability** through a combination of **cryptographic hashing** and **consensus mechanisms**.  
The **Keccak-256** algorithm is used to create unique identifiers and checksums for data — forming Merkle Tree roots and linking blocks together.  

Because each new block **“locks in” the previous one** through its hash, any attempt to rewrite history would require enormous computational resources and would be instantly detected.  
This makes the Ethereum blockchain a **reliable and immutable ledger**.

In summary, Ethereum relies on **Keccak-256**, a variant of **SHA-3**, used for:
- Hashing blocks and transactions;
- Generating addresses (from public keys);
- Building Merkle trees.  

Hashing guarantees **immutability** — any modification to data changes the hashes and breaks the chain.

---

## **5. Network Type**
Ethereum is a **public blockchain network**, meaning:
- Anyone can join the network;
- Users can run full or light nodes;
- All blockchain data (transactions, contracts, balances) is transparent and verifiable via tools like **Etherscan**.

---

## **6. Permission Model**
Ethereum operates as a **permissionless network**, meaning:
- No registration or approval is required;
- All participants are treated equally by the protocol;
- Transactions are verified automatically by nodes.  

Anyone can:
- Create an address;
- Send transactions;
- Deploy and interact with smart contracts.  

This openness guarantees **decentralization**, **transparency**, and **resistance to censorship**.
