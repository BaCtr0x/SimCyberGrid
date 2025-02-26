Server Message Block (SMB) is a network file-sharing protocol that allows applications and users to access files, printers, and other resources over a network. It is primarily used in Windows-based environments but also supports Linux/macOS through implementations like Samba.

SMB enables users to:
- Access remote files and folders as if they were local.
- Share printers and network devices across systems.
- Communicate between client and server applications over a LAN.

### How SMB Works
**SMB follows a client-server model, where:**
- A client (e.g., Windows, macOS, Linux) requests access to shared resources.
- A server (e.g., Windows Server, Samba) responds to requests and grants access.

**SMB Communication Process**
1. Client sends a request (e.g., open file, list directory) to the SMB server.
2. Server verifies authentication (username/password, Kerberos, NTLM).
3. Server grants or denies access based on permissions & ACLs.
4. Client interacts with files/printers over SMB as if they were local.
5. Connection remains open until explicitly closed.

### SMB Protocol Versions
| SMB Version | Year                           | Features & Improvements                                    |
| ----------- | ------------------------------ | ---------------------------------------------------------- |
| SMBv1       | 1980s                          | Basic file sharing, no encryption (vulnerable to exploits) |
| SMBv2       | 2006 (Windows Vista)           | Improved performance, reduced commands, better security    |
| SMBv3       | 2012 (Windows 8, Server 2012)  | Ent-to-End encrytion, better authentication                |
| SMBv3       | 2015 (Windows 10, Server 2016) | Stronger entryption (AES-GCM), improved security           |

**Why SMBv1 is Insecure**
- Lacks encrytion $\rightarrow$ Data transmitted in plaintext.
- Susceptible to Man-in-the-Middle (MITM) attacks.
- Vulenrable to exploits like EternalBlue (used in WannaCry ransomware).
- Microsoft disabled SMBv1 by default in Windows 10/Server 2016+.

### SMB Security Risks
1. SMB Relay & Man-in-the-Middle (MITM) Attacks
	- Attackers intercept authentication requests and relay credentials to access SMB shares.

2. SMB Brute Force Attacks
	- Hackers use tools like Hydra or Medusa to guess SMB login credentials.

3. Ransomware & Worms (WannaCry, NotPetya)
	- Exploits like EternalBlue allow remote execution of malware over SMB.
	- WannaCry ransomware used SMBv1 vulnerabilities to spread globally.

4. Unencrypted Communication
	- SMBv1 & SMBv2 send data unencrypted, making them vulnerable to packet sniffing.

### SMB Alternatives
| Protocol | Description|
|----------|------------|
| NFS (Network File System) | Used in Unix/Linux for file sharing |
| FTP/SFTP (Secure File Transfer Protocol) | Used for secure file transfers |
| RDP (Remote Desktop Protocol) | Used for remote access to Windows |
| WebDAV | Web-based file sharing alternative |

