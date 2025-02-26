**Transport Layer Security (TLS)** is a cryptographic protocol that provides **secure communication** over a network by ensuring **confidentiality, integrity, and authentication**. It is widely used in **HTTPS, email encryption, VoIP, and VPNs**. TLS replaces **SSL** and is more secure due to stronger encryption algorithms and better handshake mechanisms.

### How TLS Works
TLS operates using a **handshake process** to establish a **secure connection** and then encrypts data transmission.

**1. TLS Handshake (Session Establishment)**
The handshake is critical for authentication and key exchange.

1. **Client Hello**
	- The client sends a **“ClientHello”** message containing:
	- TLS **version** (e.g., TLS 1.2, TLS 1.3)
	- **Cipher suites** (AES-GCM, ChaCha20, etc.)
	- **Supported extensions** (ALPN, SNI, OCSP stapling)
	- A **random number (Client Random)** for entropy
	
2. **Server Hello**
	- The server responds with a **“ServerHello”** message containing:
	- Chosen **TLS version**
	- Selected **cipher suite**
	- **Server Random** (another random number)
	- **Digital certificate** (X.509) signed by a CA
	
3. **Server Certificate & Authentication**
	- The server provides an **X.509 certificate** to prove its identity.
	- The client **validates** the certificate using the **CA’s public key**.
	- In **mutual TLS (mTLS)**, the server also requests a **client certificate**.
	
4. **Key Exchange & Session Key Generation**
	- TLS 1.2: Uses **RSA key exchange** or **Diffie-Hellman (DH/ECDH)**.
	- TLS 1.3: Uses **Ephemeral Diffie-Hellman (ECDHE)** for perfect forward secrecy (PFS).
	- Both client and server **derive a shared session key** using the **Pre-Master Secret** and both random values.
	
5. **Finished & Session Established**
	- Both parties send a **Finished** message encrypted with the session key.
	- From this point, all data is encrypted using symmetric cryptography.

### Data Encryption (Secure Communication)
Once the handshake is complete, data is encrypted using **symmetric encryption**:
- **AES-GCM (TLS 1.2 & 1.3)**
- **ChaCha20-Poly1305 (TLS 1.3, optimized for mobile & low-power devices)**
- Encryption is done using the **session key** derived in the handshake.

### Data Integrity & Authentication
TLS ensures data integrity using **Message Authentication Codes (MACs)**:
- **HMAC (TLS 1.2)**: Hash-based integrity check (e.g., HMAC-SHA256).
- **AEAD (TLS 1.3)**: Authenticated Encryption with Associated Data (e.g., AES-GCM).

Each message has a **MAC or AEAD tag**, ensuring it hasn’t been altered in transit.

### TLS Versions & Differences
| **Version**       | **Key Features**                                                      |
| ----------------- | --------------------------------------------------------------------- |
| **TLS 1.0 & 1.1** | Deprecated due to weak ciphers & vulnerabilities.                     |
| **TLS 1.2**       | Still widely used; supports AES-GCM, HMAC, RSA/ECDH key exchange.     |
| **TLS 1.3**       | Removes insecure algorithms, enforces PFS, uses AEAD encryption only. |

### Why Use TLS?
✔ **Encrypts Data** → Prevents eavesdropping (MITM attacks).
✔ **Ensures Integrity** → Detects tampering with messages.
✔ **Authenticates Identity** → Prevents impersonation & phishing.
✔ **Enforces Perfect Forward Secrecy (PFS)** → Uses ephemeral keys (TLS 1.3).