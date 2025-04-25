The sunburst attack is also known as the SolarWinds supply chain attack and is one of the most sophisticated and high-impact cyber-espionage campaigns ever publicly disclosed. It combined nation-state level OPSEC, software supply chain compromise and stealth post-exploitation tactis.

## High-Level Attack Chain
| Stage                      | Description                                                          |
| -------------------------- | -------------------------------------------------------------------- |
| **Initial Compromise**     | Attackers breached SolarWinds’ development environment               |
| **Supply Chain Injection** | Malicious code (SUNBURST) inserted into signed Orion updates         |
| **Propagation**            | Customers downloaded trojanized updates via legitimate channels      |
| **C2 & Persistence**       | SUNBURST beaconed to attacker infrastructure; enabled further access |
| **Second-stage Payloads**  | Dropped post-exploitation malware like **Teardrop**                  |
| **Data Exfiltration**      | Conducted long-term espionage operations within selected networks    |


## Technical Breakdown
### Supply Chain Compromise
- Attackers gained access to SolarWinds' build system
- Injected malicious .NET DLL into SolarWinds.Orion.Core.BusinessLayer.dll
- The DLL was compiled and digitally signed using SolarWinds' legitimate certificate
- Updates containing the trojan were delivered via normal update mechanisms (MSI packages)
File hashes of trojanized builds were indistinguishable from legitimate ones - supply chain compromise at the binary level

### Sunburst Backdoor Behavior
#### Activation & Sleep Delay
- Backdoor doesn't activate for 12-14 days after install
- Uses environment check to avoid snadboxes:
	- Check domain names
	- Monitors running processes
	- Avoids known forensic/debug environments
#### C2 Beaconing
- Uses HTTP GET requests to subdomains under \*.avsvmcloud[.].com
- Beacon payload encoded via domain name (CNAME/DNS techniques)
- Example:
```
GET /swip/upd/SolarWinds.Orion.Core.BusinessLayer.dll HTTP/1.1
Host: abc123.avsvmcloud.com
```

#### DNS-based Command & Control
- Domains dynamically resolved by attacker-controlled nameserver
- if the target is interesting, attacker responds with a CNAME pointing to attacker C2
- Otherwise, the beacon is ignored, leaving minimal forensic trail

#### Domain Generation Algorithm (DGA)-like behavior
- Randomized subdomains used to evade static detection

### Lateral Movement & Privilege Escalation
Once inside a network (but only in high-value targets)
- Second-stage malware like:
	- Teadrop: Cobald Strike-style memory-only loader
	- Raindrop: Used in some lateral cases
- [[Mimikatz]], Token impersonation, Kerberoasting, Golden Ticket
- Abuse of [[SAML]] tokens (Golden SAML attack):
	- Forged SAML assertions via access to ADFS private key
	- Used to impersonate arbitrary users across federated identity systems (esp. in Microsoft 365/Azure AD)

### Data Exfiltration & Persistence
- Lateral movement focused on:
	- Email (Exchange, M365)
	- Source code repositories
	- Sensitive documents (policy, identity, legal)
- Exfiltration via encrypted HTTPS to C2 infrastructure
- Persistence via:
	- Scheduled tasks
	- Custom backdoors (beyond Sunburst)
	- Leveraging federated authentication for long-term access


## Advanced Evasion Techniques
|Technique|Purpose|
|---|---|
|**Delayed execution (sleep logic)**|Avoid sandbox detection|
|**Domain fronting / CNAME redirection**|Dynamic targeting control|
|**Code signed by trusted certs**|Avoid AV/EDR flagging|
|**In-memory payloads (Teardrop)**|Avoid disk forensics|
|**Golden SAML**|Long-term cross-cloud persistence|
|**Custom protocol stacks**|Blended in with Orion network telemetry traffic|

## Strategic Impact
- Attackers limited their post-exploitation scope - most of the 18 000 targets saw no second stage activity
- Operated for months undetected
- Demonstrated deep knowledge of enterprise identity infrastructure
- Highlighted the insecurity of software supply chains, especially:
	- Build pipelines (CI/CD)
	- Code signing
	- Third-party vendor trust

## Tools Detected in Use
- SUNBURST: Initial backdoor
- Teardrop/Raindrop: Custom Cobald Strike-like droppers
- Imppackt, PsExec, Mimikatz: Post-exploitation tools
- Azure/M365 abuse:
	- PowerShell, Graph API
	- Golden SAML (forged tokens)
	- Illicit consent grant via OAuth

## Detection & Response
### Indicators:
- Suspicious Orion DLLs (SolarWinds.Orion.Core.BusinessLayer.dll)
- Outbound traffic to avsvmcloud[.].com
- Abnormal SAML assertion logs
- Uknown OAuth app consents

### Mitigation:
- Isolate Orion servers immediately
- Rotate ADFS signing certificates
- Audit SAML trust relationships
- Monitor for new federated logins

