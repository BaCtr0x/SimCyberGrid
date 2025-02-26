Telnet (TELecommunication NETwork) is a protocol that allows remote access to a computer or network device over a TCP/IP network. It enables users to execute commands on a remote machine as if they were physically present at the system.

Telnet was widely used in the early days of the internet for remote administration, file access, and troubleshooting. However, due to serious security vulnerabilities, it has largely been replaced by SSH (Secure Shell).

### How Telnet Works

#### 2.1. Basic Functionality
Telnet uses a client-server model:
1. A Telnet client initiates a connection to a Telnet server over port 23.
2. The user logs in with a username and password.
3. The client sends keystrokes to the remote system.
4. The server executes commands and returns output to the client.

Telnet provides text-based access, allowing users to control the remote machine through a command-line interface (CLI).

Telnet Communication Process

**Step 1: Establishing a Connection**
- A client connects to a remote system using:
	```
	telnet <IP Address> <Port>
	```
- By default, Telnet uses port 23, but custom ports can be specified.

**Step 2: Authentication**
- The remote server prompts for a username and password.
- Since Telnet transmits credentials in plaintext, attackers can easily intercept them.

**Step 3: Command Execution**
- The user can now execute shell commands on the remote machine.
- Output is displayed on the client’s screen.

**Step 4: Termination**
- To end a Telnet session, the user types:
	```
	exit
	```

### Key Features of Telnet
| Feature | Description |
| --------- | ------------- |
| Remote Access | Allows users to access and control network devices remotely. |
| Text-Based Interface | Works in a command-line environment. |
| Unencrypted Communication | Transmits data, including login credentials, in plaintext. |
| TCP/IP Based | Operates on port 23 using the TCP protocol. |
| Multipurpose | Used for network device configuration, server access, and debugging. |

### Security Risks of Telnet
Telnet is highly insecure because it does not encrypt data. Major security vulnerabilities include:

| Security Risk | Description |
| --------------- |------------- |
| Plaintext Transmission | Telnet sends data unencrypted, making it vulnerable to eavesdropping. |
| Password Sniffing | Attackers can intercept credentials using tools like Wireshark. |
| Man-in-the-Middle (MITM) Attacks | Hackers can modify or inject malicious commands in transit. |
| Session Hijacking | Attackers can steal an active session and gain full control over the system. |
| Brute Force Attacks | Since Telnet lacks strong authentication, attackers can guess weak passwords. |

### Why Telnet is Obsolete & Replacements
Due to its security flaws, Telnet has been phased out and replaced by secure alternatives:

| Protocol | Security Features |
|----------|-------------------|
| SSH (Secure Shell) | Encrypted communication, strong authentication, secure key exchange. |
| RDP (Remote Desktop Protocol) | Provides GUI-based remote access with encryption. |
| HTTPS-based Web Interfaces | Used for managing network devices securely. |

### Telnet vs. SSH – Key Differences
| Feature | Telnet | SSH |
| --------- | -------- | ----- |
| Encryption | ❌ No encryption (plaintext) | ✅ Fully encrypted |
| Authentication | ❌ Basic (username/password) | ✅ Strong authentication (passwords, keys, certificates) |
| Port | 23 | 22 |
| Security | ❌ Vulnerable to sniffing, MITM attacks | ✅ Secure against eavesdropping |



