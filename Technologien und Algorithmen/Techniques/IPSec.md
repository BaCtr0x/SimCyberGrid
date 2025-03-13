**IPsec (Internet Protocol Security)** is a **network security protocol suite** used to provide **encryption, authentication, and data integrity** for IP traffic. It secures communications over **private and public networks (like the internet)** by encrypting packets and ensuring they reach the correct destination without tampering.

### How IPsec Works
IPsec works by establishing a **secure tunnel** between two devices (e.g., two routers, a VPN client and a server). It protects data **at the network layer (Layer 3)** of the OSI model, making it highly secure for **VPNs, remote access, and site-to-site connections**.

IPsec operates in **two main phases**:
1. **Key Exchange & Authentication (IKE Phase 1)**
	- Devices establish a secure, authenticated connection.
	- Uses **Internet Key Exchange (IKE)** protocol to set up the secure channel.

2. **Data Encryption & Transfer (IKE Phase 2)**
	- Once authenticated, devices encrypt and transmit data securely.
	- Uses security algorithms like **AES, 3DES, SHA-256** for encryption & integrity.
### IPsec Modes
IPsec operates in two different modes, depending on the use case:
1. **Transport Mode**
	- Only **encrypts the data payload** of an IP packet.
	- The original IP header is **not** encrypted (useful for internal traffic security).
	- Commonly used for **host-to-host communication**.

2. **Tunnel Mode**
	- Encrypts **both the payload and the IP header**.
	- The entire packet is **wrapped inside a new IP header**, making it completely hidden.
	- Used in **VPNs and site-to-site secure tunnels**.

### IPsec Protocols
IPsec uses a combination of **three core protocols**:
1. **Authentication Header (AH)**
	- Ensures **data integrity and authentication** (prevents spoofing).
	- Does **NOT** provide encryption—only verifies the sender’s identity.
	
2. **Encapsulating Security Payload (ESP)**
	- **Encrypts the data** for confidentiality.
	- Also provides authentication and integrity.
	- **ESP is commonly used in VPNs**.
	
3. **Internet Key Exchange (IKE)**
	- Manages the **key exchange** process between devices.
	- Ensures a secure session before encrypting traffic.
	- Uses **Diffie-Hellman key exchange** for secure encryption key generation.

### Why Use IPsec?
✔ **Strong Security** → Encrypts and authenticates data.
✔ **Prevents Eavesdropping** → Protects against MITM ([[Man in the Middle|Man-in-the-Middle]]) attacks.
✔ **Ensures Data Integrity** → Detects and blocks tampered packets.
✔ **Supports VPNs** → Used for **remote access VPNs and site-to-site tunnels**.
✔ **Works with IPv4 & IPv6** → Provides security across modern networks.