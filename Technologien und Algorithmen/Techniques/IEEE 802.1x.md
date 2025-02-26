**IEEE 802.1X** is a **network access control (NAC) protocol** that provides authentication before allowing devices to connect to a wired or wireless network. It is commonly used in enterprise environments to **secure network access** by ensuring that only **authorized users and devices** can connect.

![[IEEE_802.1x.png]]

### How IEEE 802.1X Works
IEEE 802.1X uses a **three-party authentication model** to control access:
1. **Supplicant (Client Device)**
	- The device (laptop, phone, etc.) trying to connect to the network.
	- Must provide **valid credentials** to gain access.

2. **Authenticator (Network Device)**
	- A switch (wired) or an access point (wireless) that controls access.
	- Acts as a **gatekeeper**, forwarding authentication requests.
	
3. **Authentication Server ([[RADIUS]] Server)**
	- A server that verifies the credentials (e.g., a RADIUS server like FreeRADIUS or Cisco ISE).
	- Grants or denies access based on authentication policies.
### Step-by-Step Authentication Process
1. **Connection Attempt**:
	- The supplicant (client device) tries to connect to the network.
	- The authenticator (switch/AP) detects the connection and starts authentication.
	
2. **Request for Credentials**:
	- The authenticator sends an **EAP (Extensible Authentication Protocol) request** to the supplicant.
	
3. **Supplicant Sends Credentials**:
	- The supplicant provides **a username and password or a security certificate**.
	
4. **Authenticator Forwards to Authentication Server**:
	- The authenticator **forwards** the credentials to the authentication server ([[RADIUS]] server).
	
5. **Authentication Decision**:
	- The authentication server **verifies the credentials**:
	- If valid → The user/device is **granted access**.
	- If invalid → The connection is **denied**.
	
6. **Secure Connection Established**:
	- If authentication is successful, the **network port is opened**, and the device is allowed to communicate.

### Authentication Methods (EAP Variants)
IEEE 802.1X supports multiple authentication methods using **EAP (Extensible Authentication Protocol)**, including:
- **EAP-[[TLS]] (Transport Layer Security)** → Uses digital certificates (highly secure, no passwords needed).
- **EAP-PEAP (Protected EAP)** → Uses a username/password inside an encrypted tunnel.
- **EAP-TTLS (Tunneled TLS)** → Similar to PEAP but more flexible with authentication methods.


### Why is IEEE 802.1X Important?
✔ **Enhances Security** → Prevents unauthorized access to networks.
✔ **Prevents Network Attacks** → Blocks rogue devices and unauthorized users.
✔ **Supports Centralized Authentication** → Works with RADIUS servers for efficient management.
✔ **Works for Both Wired & Wireless Networks** → Ensures secure access control for all connections.

### Use Cases
- **Enterprise Networks** → Ensures only employees’ devices can connect.
- **University Wi-Fi** → Controls student and staff access to the network.
- **Data Centers** → Prevents unauthorized devices from accessing critical systems.