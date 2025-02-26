A Drive-By Compromise is a cyberattack where a victim’s device is infected without any direct user interaction, simply by visiting a malicious or compromised website. Unlike traditional malware infections that require users to download or open files, drive-by attacks can exploit browser vulnerabilities, outdated plugins, and unpatched software to silently install malware.

This type of attack is widely used for spyware, ransomware, cryptojacking, keyloggers, and botnets.

### How Does a Drive-By Compromise Work?
**Step 1: Malicious Website or Compromised Legitimate Site**
- The attacker either:
- Creates a fake website specifically designed to deliver malware.
- Injects malicious code into a trusted website (e.g., through cross-site scripting (XSS) or a supply chain attack).

**Step 2: Exploit Kit Scans for Vulnerabilities**
- Once a user visits the infected site, a malicious script runs in the background to analyze:
- Browser version
- Operating system
- Installed plugins/extensions
- Security settings
- If the system has unpatched vulnerabilities, the exploit kit delivers payloads to execute the attack.

**Step 3: Silent Malware Execution**
- The attack automatically installs malware without requiring user interaction.
- Common payloads include:
- Remote Access Trojans (RATs) – Allow attackers to control the system remotely.
- Keyloggers – Record keystrokes to steal credentials.
- Ransomware – Encrypts files and demands payment.
- Cryptojackers – Use system resources to mine cryptocurrency.
- Botnet Malware – Adds the device to a network of infected machines for DDoS attacks.

### Attack Techniques Used in Drive-By Compromises
1. Exploit Kits (EKs)
	- Exploit Kits are automated hacking tools that detect and exploit software vulnerabilities.
	- Common exploit kits include:
	- RIG Exploit Kit (targets Internet Explorer vulnerabilities)
	- Magnitude Exploit Kit (used for ransomware distribution)
	- Fallout Exploit Kit (often deploys banking trojans)

2. Malvertising (Malicious Advertising)
	- Attackers buy ad space on legitimate websites and embed malicious code in online ads.
	- The user doesn’t need to click—simply loading the ad triggers the exploit.

3. Watering Hole Attacks
	- Attackers infect websites frequently visited by their target (e.g., government or corporate portals).
	- Employees or executives visiting the compromised site get infected.

4. Zero-Day Exploits
	- Attacks use zero-day vulnerabilities (unknown software flaws) before vendors release patches.
	- Highly dangerous, as no security updates exist at the time of attack.

### Who is Most at Risk?
- Outdated software users (Browsers, Flash, Java, PDF readers).
- Corporate employees (Targeted in watering hole attacks).
- Government & military personnel (Often victims of nation-state APTs).
- Users without ad blockers or security tools (Malvertising victims).
- Regular web users (Unknowingly visiting infected sites).

### How to Detect Drive-By Compromises?
**Behavioral Indicators**
- Unexpected slowdowns (Cryptojacking silently using CPU power).
- Strange network activity (Malware communicating with C2 servers).
- Random pop-ups or redirects (Possible browser hijacking).
- Unauthorized software installations (Malware downloaded silently).

**Technical Detection**
- Endpoint Detection & Response (EDR) – Identifies suspicious processes.
- Network Traffic Analysis – Detects unusual outbound connections.
- Threat Intelligence Feeds – Alerts for known drive-by malware campaigns.
- Honeytokens – Detects compromised sessions.

### Prevention & Security Best Practices
**For Individuals**
- Keep browsers & plugins updated – Prevent exploits by patching vulnerabilities.
- Disable unnecessary plugins (Flash, Java) – These are common attack vectors.
- Use ad blockers (uBlock Origin, AdGuard) – Prevent malvertising threats.
- Enable browser security settings – Block pop-ups, disable auto-downloads.
- Avoid suspicious sites – Stick to HTTPS and reputable domains.
- Use script-blocking extensions (NoScript, uMatrix) – Prevent unauthorized scripts from executing.

**For Organizations**
- Deploy Web Application Firewalls (WAFs) – Protect corporate sites from infection.
- Network Segmentation – Isolate infected machines to limit malware spread.
- Monitor Traffic Logs (SIEM Solutions) – Detect suspicious web activity.
- Implement DNS Filtering – Block known malicious domains.
- Regular Security Awareness Training – Educate employees about drive-by threats.
- Endpoint Protection (EDR/XDR Solutions) – Detect and block exploit attempts.


