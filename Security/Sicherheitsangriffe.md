## MEDIT
### Typische Angriffsvektoren
- Fokus auf IKT-Montoring und Intrusion Detection
- Gewachsene Infrastruktur häufiger noch alte, unsichere Zugriffsverfahren, somit sowas wie Telnet-Verbindungen berücksichitgen
- Interne oder externe Angriffe die Zugriffe zu IKT-Netz verschaffen
	- Bsp. abgelegene Ortsnetzstation. Dort äußere Sicherhietssysteme mit Netz über eibruch kommunizieren damit Station aus Netz genommen werden kann.
	- Entspricht Prinzip Security-in-depth
	- Schnell erkennen ob alle Dienste im IKT-Netz verfügbar sind und Abweichungen schnell erkannt und Abschnitte-Teile reaktiveiren
- Scenarien:
	1. Detection und Unterbindung eines Angriffs mittels Access Control Detection
	2. $(a-d)$ Testfaelle fuer Verwendung unsicherer Protokolle auf die Intrusion Detection System (IDS) reagieren soll
	3. $(a-d)$ Mengelnde Sicherheit durch den viel genutzten Standard IEC-60870-5-104. Das Protokoll ist fuer Austausch von Schaltbefehlen, Messwerten und Konfigurationen zwischen Leitwartensystem und entfernter Unterstation
	4. Brute-Froce-Angriffe auf einer im IKT-Netz befindliche Router
### Strukturierte mehrstufige Angriffsscrenarien
#### Initial Access
- **Haeufigste Technik:** Phishing (z.B. [[Spear_Phishing]])
- **Ziel:** Schadcode auf Zielsystem ausfuehen oder Zugangsdaten stehlen
- **Weitere Methoden:** [[Drive by Compromise]], Lieferketten-Kompromierung
- wird oft asl erster Schritt fuer mehrstufige Angriffe genutzt

#### Execution
- Nutzung von Scriptinterpretern und Befehlen zur Codeausfuehrung
- **Benutzerausfuehrung:** opfer oeffnet und fuehrt eine manipulierte Datei aus
- Client-Schwachstellen werden gezielt ausgenutzt (z.B. durch Phishing)
- Task-Scheduling fuer geplante Schadcode-Ausfuehrung oft fuer Persistenzzwecke

### Credential Access
- **OS Credential Dumping:** Abgreifen von Anmeldedaten direkt aus dem Betriebssystem
- Keylogging oder Phishing zur Gewinnung von Anmlededaten
- Haeufig genutzte fuer weiterfuehrende Angriffe auf interne Netzzwecke

### Lateral Movement
- **Remote Service Exploitation:** Angreifer nutzen Schwachstellen in Remote Service (z.B. SMB,RDP)
- **Pass-the-Hash & Pass-the-Ticket:** Verwendung gestohlener Hashes fuer Authentifizierung
- Remote Code Execution (RCE) ueber Netzwerkdienste zur Ausbreitung der Maleware
- **Exploitation fuer Privilege Escalation:** Kombination mit Privilege Escalation fuer erhoete Rechte

### Collection
- **Ziel:** Extraction relevanter Daten fuer spaetere Angriffe oder Datendiebstahl
- Keylogging und Screen-Capturing zur Ueberwachung von Benutzeraktivitaeten
- Scanning von Dateisystemen nach sensiblen Konfigurationsdateien
- Credential Dumping zum Extrahieren von passwoertern und Hashes aus Betriebssystem
- Network Shifting zur Analyse von Kommunikationsdaten und Passwoertern

### Command and control (C2)
- **Ziel:** Aufrechterhaltung von Kontrolle ueber Kompromitierte Systeme
- Nutzung von HTTPS und DNS-Tunneling um Erkennung von Firewall zu umgehen
- Dynamische Domain-Generierung (DGA) zur Erschwerung der Blockierung durch Sicherheitsmeachnismen
- Fallback-Kanaele (z.B. ueber ICMP oder SMTP) zur Sicherstellung der Kommunikation
- Nutzung legitimer Remote Access Tools (RATs) zur Steuerung infizierter Hosts
### Impact
- **Ziel:** Manipulation, Sabotage oder Zerstoerung von Systemen oder Daten
- **ICS-Manipulation:** Faelschnung oder Veraenderung von Messwerten und Steuerbfehlen
- Datenloeschung (Wipe-Angriff) zur Sabotage von IT- und SCADA-Systemen
- Denial-of-Service (DoS) zur Ueberlastung und Lahmlegung von Netzwerken
- Manipulation von Sicherheitssystemen um Angriffe zu verschleiern


## SGCG
### Attackvectors
#### Unauthorized Access / Intrusion
- Attackers gain unauthorized access to the smart grid infrastructure.
 - **Impact:** Can lead to system manipulation, data theft, or disruptions.
#### Denial of Service (DoS)
- Attackers flood communication channels or overload system resources.
- **Impact:** Grid operations and real-time communications may be deleyed or completely shut down, affecting reliability.
#### Man-in-the-Middle (MITM) Attacks
- Attackers intercept or alter communications between grid components.
- **Impact:** Can lead to data corruption, operational failures, and incorrect grid status reporting.
#### Malware and Ransomware
- Malicious software is introduced to the grid, potentially encrypting critical data.
- **Impact:** Grid operators may lose access to key control systems, demanding ransom or causing operational delays.
#### Data Manipulation and Spoofing
- Attackers alter transmitted data or inject fake data into the system.
- **Impact:** Grid operators receive incorrect information, leading to improper decision-making and potential system failures.
#### Compromised Smart Meters
- Attackers gain control of smart meters to alter billing data or cause system instabilities.
- **Impact:** Revenue loss, incorrect billing, and potential cascading failures in the grid.
#### Supply Chain Attacks
- Attackers compromise vendors or third-party suppliers to introduce vulnerabilities.
- **Impact:** Backdoor access to the grid network, leading to system-wide exploits.
#### Lack of Encryption and Weak Authentication
- Insecure communication channels or weak credentials allow unauthorized access.
- **Impact:** Eavesdropping, interception of control commands, and data breaches.
#### Phishing and Social Engineering
- Cybercriminals trick employees into disclosing sensitive credentials.
- **Impact:** Leads to unauthorized access and potential grid sabotage.
#### Firmware and Software Vulnerabilities
- Exploiting unpatched firmware or outdated software.
- **Impact:** System takeover, operational failures, and unauthorized control of grid elements.
### Impact of These Attacks
#### Grid Instability and Blackouts
- Attacks on critical control systems could lead to power outages or cascading failures.
#### Financial Losses
- Manipulated billing systems, energy theft, and ransom demands can result in economic losses.
#### Data Breaches and Privacy Violations
- Customer and operational data leakage could lead to identity theft or industrial espionage.
#### Physical Damage
- Attacks on automated systems could lead to malfunctioning hardware or equipment failures.
#### Regulatory and Legal Consequences
- Violations of cybersecurity regulations may lead to fines and legal repercussions.

## SGCG Security Paper 
### Security Attacks and Their Associated Impacts
The report presents a layered threat and impact assessment model using four specific Smart Grid use cases, with particular focus on the **Distributed Energy Resources (DER) Control Use Case**, **Substation Automation**, and **Control Center Operations**. It identifies potential cyber-attack scenarios that may compromise smart grid operations at different levels. These scenarios are categorized by target, potential impact (energy loss), and consequences for grid operations and societal infrastructure.
#### Attacks on DER Control Systems
- **Target:** DER controllers, field devices, and communication infrastructure
- **Impact:** Disruption of DER control may lead to a **loss of energy supply up to 100 MW**
- **Scale of Disruption:** Local to regional (e.g., town or small region)
- **Impact on Critical Infrastructure:**
    - May affect industrial zones, public services, or transport hubs relying on distributed generation

- **Impact on Population:**
    - Moderate, depending on dependency on DER-supplied power

- **Risk Level:** **Medium**
- **Security Level (SGIS-SL):** Typically mapped to **Level 2** (Medium)

---
#### Attacks on Substation Automation and Communication Networks
- **Target:** Intelligent Electronic Devices (IEDs), Substation Gateways, SCADA links
- **Impact:** Could result in **power outages ranging from 100 MW to 1 GW**
- **Scale of Disruption:** Regional to national (e.g., major metropolitan areas)
- **Impact on Critical Infrastructure:**
    - High – may cause cascading failures or faults in protection systems
    - Impacts may include failure of water supply, telecommunications, or emergency services

- **Impact on Population:**
    - High, especially during peak usage or emergencies

- **Risk Level:** **High**
- **Security Level (SGIS-SL):** **Level 3–4** (High to Critical)

---
#### Attacks on Control Center or Centralized Management Systems
- **Target:** Distribution Management Systems (DMS), Energy Management Systems (EMS), and central command platforms
- **Impact:** Catastrophic failure of energy distribution management with potential **power losses of 1 GW to 6 GW or more**
- **Scale of Disruption:** National or multi-national (Pan-European potential)
- **Impact on Critical Infrastructure:**
    - **Critical** – potential blackout across large regions, major threat to public safety and national security

- **Impact on Population:**
	- Very high – affecting millions of individuals, essential services, and critical infrastructure

- **Risk Level:** **Very High**
- **Security Level (SGIS-SL):** **Level 4–5** (Critical)

---
### Identified Cybersecurity Attack Vectors
The report outlines several **attack vectors** that adversaries could exploit to compromise smart grid operations:
#### Communication Interfaces
- **Substation-DER and Control Center-Field Devices Interfaces**
- These interfaces are vulnerable due to inadequate segregation or weak authentication.
- Attackers can intercept or manipulate data traffic to induce false readings, disable assets, or issue unauthorized commands.
- **Impact:** Medium to high, depending on system criticality.

---
#### Standard Protocol Exploits
- **GOOSE, MMS (IEC 61850)** and **ICCP (TASE.2)** are widely used protocols in substations and control centers.
- If not properly secured (e.g., via IEC 62351), they may be exploited for replay, injection, or denial-of-service (DoS) attacks.
- **Impact:** Unauthorized control actions or substation outages.

---
#### Centralized Network Breach
- Unauthorized access to central control systems can allow attackers to manipulate grid topology, falsify data, or disable safety interlocks.    
- **Impact:** Critical – can compromise wide-area control operations.

---
#### Remote Access and Maintenance Interfaces
- Use of VPNs, web portals, or poorly configured remote diagnostic interfaces can serve as backdoors.
- **Impact:** High – allows attackers to bypass perimeter defenses.

---
#### Insider Threats and Social Engineering
- Personnel with legitimate access may be manipulated or may act maliciously.
- Lack of role-based access control and weak audit mechanisms heightens this risk.        
- **Impact:** Varies from localized misconfiguration to full system breach.    

---
### Summary Table of Security Levels and Impacts

|**Attack Target**|**Attack Vector**|**Impact Level**|**Potential Energy Loss**|**Scale of Impact**|**SGIS Security Level**|
|---|---|---|---|---|---|
|DER Network|Protocol manipulation, unauthorized commands|Medium|≤ 100 MW|Town / Region|Level 2|
|Substation Automation Systems|IED hijacking, GOOSE/MMS exploits|High|100 MW – 1 GW|Regional / National|Level 3–4|
|Control Center Operations|Central network compromise, DMS/EMS disruption|Critical|1 GW – 6 GW+|National / Pan-European|Level 4–5|
