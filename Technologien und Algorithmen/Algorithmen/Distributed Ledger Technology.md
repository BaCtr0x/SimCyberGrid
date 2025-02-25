### Definition
**Distributed Ledger Technology (DLT)** is a decentralized system where data is replicated, shared, and synchronized across multiple nodes in a network. Unlike traditional databases, DLT eliminates the need for a central authority, enhancing transparency, security, and fault tolerance.

### Characteristics
- **Decentralization:** No single point of control or failure.
- **Consensus Mechanisms:** Transactions are validated through protocols like Proof of Work (PoW) or Proof of Stake (PoS).
- **Immutable & Tamper-Resistant:** Once recorded, data cannot be altered without network consensus.
- **Transparency:** All participants have access to the ledger, improving trust.
- **Cryptographic Security:** Transactions are encrypted and linked using cryptographic hashes, commonly used is [[ECDSA]].

### Mode of Operation
- **Transaction Proposal:** A node submits a transaction request.
- **Validation & Consensus:** Other nodes verify and agree on transaction validity using a consensus mechanism.
- **Ledger Update:** The validated transaction is added to the distributed ledger and synchronized across all nodes.
- **Immutable Record:** Transactions are permanently stored, preventing unauthorized modifications.

### Types of DLTs
- **[[Blockchain]]:** Uses a chain of cryptographically linked blocks (e.g., Bitcoin, Ethereum).
- **DAG (Directed Acyclic Graph):** Transactions form a web-like structure instead of blocks (e.g., IOTA's Tangle).
- **Hashgraph:** Uses a gossip protocol for consensus (e.g., Hedera Hashgraph).

### Security Risks and Challenges
- **51% Attack:** In PoW-based systems, if an entity controls over 50% of the network, they can manipulate transactions.
- **Private Key Theft:** If an attacker gains access to a private key, they can control associated assets.
- **Sybil Attack:** A single entity creates multiple fake nodes to manipulate consensus.
- **Consensus Exploits:** Weaknesses in algorithms can allow fraudulent transactions.
- **Data Privacy Issues:** Public DLTs store all transactions transparently, which may expose sensitive data.