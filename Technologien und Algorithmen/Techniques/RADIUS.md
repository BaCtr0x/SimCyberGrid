**RADIUS (Remote Authentication Dial-In User Service)** is a **network protocol** used for **centralized authentication, authorization, and accounting (AAA)**. It ensures that users and devices accessing a network are properly authenticated and tracked.

### How RADIUS Works
RADIUS follows the **AAA model**:
1. **Authentication** (Who are you?)
	- Verifies user identity using credentials (username/password, certificates, etc.).
	
2. **Authorization** (What can you do?)
	- Determines the user’s permissions and network access level.
	
3. **Accounting** (What did you do?)
	- Logs user activity for security and auditing.

### RADIUS Components
1. **Client (Supplicant)**
	- The user or device trying to connect (e.g., laptop, phone, or VPN user).
	
2. **Network Access Server (NAS) / Authenticator**
	- A device like a **Wi-Fi access point, switch, or VPN server** that acts as a gateway.
	- Sends authentication requests to the RADIUS server.
	
3. **RADIUS Server**
	- The central server that **verifies user credentials**.
	- Common RADIUS servers: **FreeRADIUS, Microsoft NPS, Cisco ISE**.
	
4. **User Database**
	- Stores user credentials (e.g., Active Directory, LDAP, or SQL database).
	- The RADIUS server checks credentials against this database.
### Step-by-Step RADIUS Authentication Process

1. **User Attempts to Connect**
	- The supplicant (e.g., laptop or VPN client) sends a login request to the NAS (e.g., Wi-Fi AP or VPN server).
	
2. **NAS Sends Authentication Request**
	- The NAS forwards the credentials (username/password, certificate) to the RADIUS server.
	
3. **RADIUS Server Verifies Credentials**
	- It checks the credentials against the **user database**.
	- If valid → Proceed to authorization.
	- If invalid → Reject the request.
	
4. **Authorization Decision**
	- The RADIUS server determines **what the user is allowed to do** (e.g., access a specific VLAN or network resource).
	
5. **Access Granted or Denied**
	- If authenticated and authorized, the RADIUS server sends an **Access-Accept** message.
	- If failed, it sends an **Access-Reject** message.
	
6. **Accounting Logs User Activity**
	- If access is granted, the RADIUS server starts tracking session details (login time, duration, data usage, etc.).


### RADIUS Protocol & Communication

- Uses **UDP** (default ports: **1812** for authentication, **1813** for accounting).
- Encrypts passwords but not the entire packet (can be secured with **[[IPsec]], [[TLS]], or VPN tunnels**).
- Supports **EAP (Extensible Authentication Protocol)** for enhanced security.

### Why Use RADIUS? 
✔ **Centralized Authentication** → Manages users from one place.
✔ **Stronger Security** → Supports multifactor authentication (MFA).
✔ **Role-Based Access** → Assigns users to VLANs or access groups.
✔ **Accounting & Auditing** → Tracks login times and network usage.