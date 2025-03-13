A Man-in-the-Middle (MITM) attack occurs when a malicious actor intercepts and possibly alters communication between two parties without their knowledge. The attacker positions themselves between the sender and receiver to steal sensitive data, inject malicious content, or impersonate one of the parties.

MITM attacks are used to:
- Steal login credentials (banking, social media, email).
- Hijack secure sessions (cookies, authentication tokens).
- Intercept financial transactions (credit card details, crypto transactions).
- Modify or inject malicious content into communications.

### How MITM Attacks Work
**Step 1: Interception (Eavesdropping)**
- The attacker sniffs traffic between two communicating devices.
- They may use packet capture tools (Wireshark, tcpdump) or compromise network infrastructure (Rogue Wi-Fi, ARP spoofing).

**Step 2: Data Manipulation (Optional)**
- The attacker may modify or inject malicious content into the intercepted communication.
- This is common in phishing, malware injection, and DNS spoofing.

**Step 3: Data Extraction or Impersonation**
- The attacker steals login credentials, financial data, or sensitive information.
- In some cases, they impersonate one of the parties to continue the attack.

### Types of MITW Attacks
| Attack Type | Description | Example |
|-------------|-------------|---------|
| Wifi Eavesdropping | Attacker sets up a fake Wifi hotspot to intercept user data | A hacker creates a "Free Starbucks Wifi" network to capture user credentials.
| ARP Spoofing (Local Network Attack) | Attacker spoofs the ARP cache to redirect network traffic through their machine | Used to intercept LAN traffic in workplaces, cafes, or public networks |
| DNS Spoofing | Attackers modify DNS response to redirect users to malicious websites | A fake google.com page is displayed to steal credentials |
| HTTPS Downgrade Attack (SSL Stripping) | Attacker forces a connection from HTTPS $\rightarrow$ HTTP to steal data in plaintext | User thinks they're on a secure banking site, but data is exposed |
| Session Hijacking (Cookie Theft) | Attacker steals session cookies to impersonate the victim | A hacker captures a Facebook session token and logs in a the user |
| Email Hijacking | Attacker intercepts corporate email exchanges and minpulates financial transactions | Business Email Compromise (BEC) to redirect wire transfers |
| VoIP MITM (Man-in-the-call) | Attackers intercept and alter Voice-over-IP (VoIP) calls | Fake customer support scam using call rerouting |

### How to Detect MITM Attacks?
1. Unexpected SSL/TLS Certificate Warnings
	- If a website that normally uses HTTPS suddenly gives a security warning, it may be a MITM attack.

2. Slow or Unstable Network Performance
	- If web pages load slowly or you experience frequent disconnections, it may indicate network interception.

3. Suspicious HTTPS-to-HTTP Downgrades
	- Check if a secure website (https://) suddenly loads as http://.

4. DNS Resolution Mismatch
	- If you type www.google.com but are redirected to a suspicious-looking website, DNS spoofing may be involved.

5. Unexpected Logouts or Session Resets
	- If your accounts are randomly logged out or you see unrecognized logins, session hijacking may have occurred.

### How to Prevent MITM Attacks?
1. Use HTTPS & Encrypted Communication
	- Always check for HTTPS (padlock icon 🔒) in the browser.
	- Use browser extensions like HTTPS Everywhere.

2. Avoid Public & Unsecured Wi-Fi
	- Never enter passwords or banking details on public Wi-Fi.
	- Use VPNs (Virtual Private Networks) to encrypt traffic.

3. Enable Multi-Factor Authentication (MFA)
	- Even if an attacker steals your credentials, MFA blocks unauthorized access.

4. Use Secure DNS (DNS over HTTPS or DNS over TLS)
	- Switch to secure DNS providers:
	```
	Google DNS: 8.8.8.8, 8.8.4.4
	Cloudflare DNS: 1.1.1.1
	Quad9 DNS: 9.9.9.9
	```

5. Verify SSL/TLS Certificates
	- Before entering sensitive data, check for a valid SSL certificate:
	```
	Click the 🔒 padlock in the browser → View Certificate Details.
	```

6. Use Secure Email & Messaging
	- Use end-to-end encrypted email (ProtonMail, Tutanota).
	- Use secure messaging apps (Signal, Telegram, WhatsApp).

7. Secure Local Networks (Prevent ARP Spoofing)
	- Use static ARP tables to prevent ARP poisoning.
	- Enable port security and dynamic ARP inspection (DAI) on enterprise routers.
