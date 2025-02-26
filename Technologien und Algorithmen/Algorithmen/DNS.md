The Domain Name System (DNS) is the internet’s phonebook, translating human-friendly domain names (e.g., google.com) into IP addresses (e.g., 142.250.190.14) that computers use to locate web servers and services.

DNS is a critical network service, enabling seamless internet navigation while also being a target for cyberattacks.

### Why is DNS Important?
- Humans remember domain names (e.g., facebook.com), but computers communicate using IP addresses (e.g., 157.240.20.35).
- DNS automates the translation process, allowing users to access websites without memorizing complex IP addresses.
- Reduces workload for users and applications by enabling dynamic IP resolution.

### How DNS Works – The Resolution Process
**Step 1: User Enters a URL**
- Example: A user types www.example.com into a browser.

**Step 2: DNS Query Initiated**
- The browser checks its local cache for a recent lookup.
- If no cached entry exists, the request goes to the DNS resolver (provided by ISP or manually set like Google DNS: 8.8.8.8).

**Step 3: Recursive DNS Resolution**
1. Recursive Resolver (ISP or third-party DNS resolver like Cloudflare 1.1.1.1) queries the root DNS server (.).
2. The root server directs the query to the TLD (Top-Level Domain) DNS server (e.g., .com for example.com).
3. The TLD server directs it to the Authoritative DNS server (which holds the actual IP address).
4. The Authoritative DNS server returns the IP address (e.g., 192.168.1.1).

**Step 4: DNS Response to Client**
- The DNS resolver caches the result for faster future lookups.
- The browser connects to the IP and loads the requested website.

### Types of DNS Servers
| Type | Function |
|------|----------|
| Recursive Resolver | Handles user queries, searches cache, or forwards to root servers. |
| Root DNS Servers | 13 global servers managing top-level domains (TLDs). |
| TLD Name Servers | Manage specific domain extensions (.com, .org, .net). |
| Authoritative Name Servers | Store the actual IP mappings for domains. |

### DNS Caching – Why It Matters?
- Speeds up browsing by storing results for future queries.
- Reduces load on DNS servers by avoiding repetitive lookups.
- Cache locations:
	1. Browser Cache (stores recent lookups).
	2. Operating System Cache (local DNS resolver cache).
	3. ISP/Resolver Cache (Google DNS, OpenDNS, Cloudflare DNS).

To clear cache:
	•	Windows: ipconfig /flushdns
	•	Mac/Linux: sudo systemd-resolve --flush-caches

### DNS Security Threats
1. DNS Spoofing (DNS Cache Poisoning)
	- Attackers inject fake DNS entries into a resolver’s cache.
	- Redirects users to malicious websites.
	- Example: google.com could be poisoned to point to a phishing site.

2. DNS Hijacking
	- ISPs or malware redirect DNS requests to rogue servers.
	- Can be used for censorship or surveillance.

3. DDoS Attacks on DNS
	- Attackers overload DNS servers with massive query requests, making websites unreachable.
	- Example: Mirai botnet attack on Dyn in 2016 disrupted Twitter, Reddit, Netflix.

4. Man-in-the-Middle (MITM) DNS Attacks
	- Attackers intercept DNS queries and alter responses.
	- Common on public Wi-Fi networks.

5. Subdomain Takeover
	- Occurs when dangling CNAME records point to expired services, allowing attackers to hijack subdomains.

### DNS Security Solutions & Best Practices
1. Use Secure DNS Resolvers
	- Switch to trusted DNS providers:
	- Google DNS: 8.8.8.8, 8.8.4.4
	- Cloudflare DNS: 1.1.1.1
	- Quad9 DNS: 9.9.9.9 (blocks malicious domains)

2. DNSSEC (DNS Security Extensions)
	- Prevents DNS spoofing and forgery by using digital signatures.
	- Ensures DNS responses haven’t been altered.

3. Use Encrypted DNS Protocols
	- DNS over HTTPS (DoH) $\rightarrow$ Encrypts DNS queries over HTTPS.
	- DNS over TLS (DoT) $\rightarrow$ Encrypts DNS queries over TLS.

4. Implement Internal DNS Filtering
	- Block known malicious domains.
	- Prevent phishing and malware infections.

5. Monitor DNS Logs for Anomalies
	- Helps detect suspicious DNS requests that might indicate malware activity or data exfiltration.