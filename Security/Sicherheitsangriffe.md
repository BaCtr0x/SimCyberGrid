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
- **Haeufigste Technik:** Phishing (z.B. [[Spear Phishing]])
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
- **Impact:** Backdoor access to the grid network, leadi| Layer                      | Action                                                                     |
| -------------------------- | -------------------------------------------------------------------------- |
| **Network Segmentation**   | Strict separation of IT/OT; no internet access to engineering workstations |
| **Protocol Whitelisting**  | Only allow expected PLC protocols and command types                        |
| **Deep Packet Inspection** | Monitor for unauthorized Modbus/FINS traffic                               |
| **Firmware Verification**  | Check PLCs for unauthorized code uploads                                   |
| **Asset Hardening**        | Disable unused services on PLCs; enforce authentication                    |rmware and Software Vulnerabilities
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

## Comprehensive Survey of Smart Grid Security (2024)

### Cyber Layer Attacks:
The cyber layer in smart grids includes network, management and application sub-layers. The different attacks outlines in the following table focus on the components in this layer.

| Attacks                    | Description                                                                                                                                                                                                                                                                                                                                                                             | Security Impact | SGAM Layer                 |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- | -------------------------- |
| Eevesdropping              | Also known as packet sniffing refers to the interception and analysis of network traffic to gain sensitive information.                                                                                                                                                                                                                                                                 | Confidentiality | Information                |
| Man-in-the-Middle          | The attacker intercepts the communication between two parties, pretending to be the other for both parties. This allows the attacker to intercept, manipulate or inject packets without being noticed.                                                                                                                                                                                  | Confidentiality | Communication              |
| Unauthorized Access        | The attacker gets illegitimate access to critical systems, which allows her to tamper with energy usage data, disrupting grid operations or gain customer information.                                                                                                                                                                                                                  | Confidentiality | Information                |
| Reconnaissance             | This is mostly a preliminary step and corresponds to scanning the network to identify critical infrastructures or passively monitor network traffic to identify potential vulnerabilities.                                                                                                                                                                                              | Confidentiality | Communication              |
| Message Replay             | With this attack the attacker captures a legitimate transmission and retransmits it to conceal malicious activities.                                                                                                                                                                                                                                                                    | Confidentiality | Information, Communication |
| Supply Chain Attacks       | This attack aims to tamper with the production of the components of the smart grid. Particularly hardware supply chain attacks aim to tamper with the production to introduce backdoors or vulnerabilities which can be used later on.                                                                                                                                                  | Integrity       | Component                  |
| Command Manipulation       | As the name suggest these attacks aim to alter commands that are being send through the network.                                                                                                                                                                                                                                                                                        | Integrity       | Function, Information      |
| Code Manipulation          | These attacks taget the software of the different components and the general network to introduce vulnerabilities or facilitate unauthorized access.                                                                                                                                                                                                                                    | Integrity       | Function, Component        |
| Malware Injection          | Malware injection inserts malicious software into the system to disrupt their functionality, steal sensitive information or facilitate future attacks.                                                                                                                                                                                                                                  | Integrity       | Function, Component        |
| Rogue Node                 | They intercept, modify or inject false data, commands or messages to directly breach the security and cause system instabilities.                                                                                                                                                                                                                                                       | Integrity       | Information                |
| Broadcast Message Spoofing | This attack specifically focuses on the [[Modbus]] protocol, but can be adapted to a more general case, in which the attacker produces a legitimate message that is being broadcast to every other party potentially distributing incorrect commands or disrupting the information flow.                                                                                                | Integrity       | Information                |
| Topology Attacks           | They provide false or misleading data of the grid topology to control systems in order to disrupt the system communication.                                                                                                                                                                                                                                                             | Integrity       | Information, Components    |
| Sybil                      | Here the attacker uses one node in the network to claim multiple identities. This allows her to disproportionally impact the network operations, manipulate data aggregation, disrupt communication or undermine trust based schemes.                                                                                                                                                   | Integrity       | Information, Component     |
| Byzantine                  | One or more nodes behave maliciously or unpredictably, undermining the system reliability.                                                                                                                                                                                                                                                                                              | Integrity       | Information, Communication |
| DOS/DDOS                   | These attacks overwhelm a target system or network, rendering it unavailable or inaccessible. They often use one device in the network to flood the network with excessive traffic or requests. The DDOS attack on the other hand coordinates multiple devices to generate a huge number of requests also flooding the communication channels and preventing relevant traffic to occur. | Availability    | Communication              |
| Response Delay             | These attacks focus on [[Modbus]] devices to intentionally increase the latency in their response disrupting real-time operations and thus creating synchronization issues, incorrect system states and even unavailability of control responses.                                                                                                                                       | Availability    | Communication              |

### Cyber-Physical Layer Attacks
This layer includes control measurement and sensor sub-layers. The following attacks exploit vulnerabilities in these layers to impact the smart grid's funtctionalities.


| Attack                                        | Description                                                                                                                                                                                                                                                                                       | Security Impact | SGAM Layer                 |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- | -------------------------- |
| Side Channel Attack                           | In this attack one can gain sensitive data through information leaks from physical systems. A simple example would be power analysis attacks, which monitor the power usage of a device to infer a secret key.                                                                                    | Confidentiality | Component                  |
| Insider Attacks                               | This attack is straight forward, were an insider with sufficient authorization access the network and smart grid system to leak information to another malicious party.                                                                                                                           | Confidentiality | Information, Communication |
| GPS Spoofing and Time Synchronization Attacks | This attack is used to trick a device into thinking it is at a different location leading to false time readings, disrupting real-time and time sensitive measurements.                                                                                                                           | Integrity       | Information                |
| False Data Injection (FDI)                    | As the name suggests the attacker aims to inject false data into the system, either to disrupt the system or to gain a monetairy or power advantage.                                                                                                                                              | Integrity       | Information                |
| Attacks on Automatic Generation Control (AGC) | The attacker induces frequency instability, overloading or underloading of generators, or even cause blackouts by preventing or manipulating the AGC system. This system maintains a real-time balance between generation and load by continually adjusting power output from various generators. | Integrity       | Component                  |
| Attacks on Voltage Control                    | These attacks aim to manipulate control systems to alter voltage levels within the grid.                                                                                                                                                                                                          | Integrity       | Component                  |
| Demand Side Management Attacks                | This attack focuses on the manipulation of pricing signals for customers in a demand response system.                                                                                                                                                                                             | Integrity       | Information                |
| Switching Attacks                             | The attacker aims to manipulate the sate of switches (e.g. circuit breakers, transfer switches) to disrupt normal grid operation and cause physical damage.                                                                                                                                       | Integrity       | Component                  |
| Load Redistribution                           | The attacker focuses on the control system in order to alter the distribution of electrical loads across the network                                                                                                                                                                              | Integrity       | Information, Component     |
| Attacks on Vehicle-to-grid (V2G)              | In this attack the malicious party takes control of an autonomous vehicle or the V2G communication interface to manipulate power flow, spoof charging/discharging commands or disrupt grid balance by injecting false data.                                                                       | Integrity       | Component                  |
| Autora                                        | This attack de-synchronizes the phase of a generator from the power grid.                                                                                                                                                                                                                         | Integrity       | Component                  |
| Advanced Persistent Threats (APTs)            | These group of attacks aim to maintain ongoing access to a targeted network for monitoring activities and breaching sensitive data.                                                                                                                                                               | Integrity       | Information, Communication |
| Source ID Mix Attacks                         | It is a type of data spoofing, where the attacker targets wide-area measurement systems in smart grids to tamper with the data from PMUs through source identification tag confusion.                                                                                                             | Integrity       | Information                |
| Rouge Interloper                              | This attack allows the attacker to infiltrate the network and get a malicious device or entity into the system. This is often done through identity spoofing or other forms of deception.                                                                                                         | Integrity       | Communication, Component   |
| Puppet Attacks                                | This one is similar to the rouge interloper, however in this case the attack does not need to add a malicious device or entity to the system but rather takes over one and uses it to perform false data injection attacks or monitoring of sensitive data.                                       | Availability    | Communication, Component   |


### Coordinated (hybrid) Attacks
The coordinated attacks combine multiple attacks more often ones from the cyber and the cyber-physical layer to increase their effectiveness or to stay hidden and maintain manipulation.


| Attack                             | Description                                                                                                                                                                             | Security Impact                          | SGAM Layer                            |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- | ------------------------------------- |
| Coordinated Data Injection Attacks | The attacker injects false data which appears to be normal grid operations and readings, resulting in incorrect control decisions and potential large-scale power outages.              | Integrity                                | Information, Communication            |
| Coordinated Load Changing Attacks  | The attacker coordinates botnets (e.g. large number of infected IoT devices) to create a sudden spike or drop in energy usage which disrupts the balance between generation and demand. | Availability                             | Communication, Component              |
| Coordinated Replay Attacks         | In this case the attacker uses replay attacks to mask the effects of physical attacks on the power grid by replaying normal meter measurements to control centers.                      | Confidentiality, Integrity               | Information, Communication, Component |
| Coordinated Topology Attacks       | These attacks manipulate state and topology data to mislead the control center about line outages, which can lead to cascading failures within the grid.                                | Integrity, Availability                  | Information                           |
| Line Outage Masking Attacks        | The attacker fools the control center into thinking the grid is operating normally despite one or more transmission lines are out of service.                                           | Integrity, Availability                  | Information, Component                |
| Coordinated DoS Attacks            | The coordinated DoS attack targets both physical infrastructure and SCADA system, resulting in severe disruptions and damage on the system.                                             | Confidentiality, Integrity, Availability | Information, Communication            |

## Milena BA:
In this thesis Florian Boehmer focuses on current security standards for microgrids and previously occurred attacks on them. Thus the mentioned attacks are not as general as in the previous section but rather focus on actually occurring attacks with their given name and year

| Attacks                                                            | Description                                                                                                                                                                                                                                                                         | Year | Type     |
| ------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---- | -------- |
| [[Black Energy 3]]                                                 | Focused attack on Industrial Control Systems using DDoS software and expanding it to include monitoring and manipulation tools.                                                                                                                                                     | 2015 | Malware  |
| [[Industroyer or CrashOverride (2016)\|CrashOverride/Industroyer]] | Used to sabotage industrial control systems of power systems. This software caused physical damage to the power infrastructure.                                                                                                                                                     | 2016 | Malware  |
| [[VPNFilter]]                                                      | This malware entered more than a hundredthousand routers and network devices in ucrain. The goal                                                                                                                                                                                    | 2018 | Malware  |
| [[Stuxnet]]                                                        | Focused on SCADA-Systems made by Siemens used in the nuclear power plant in iran. The goal was to control the centrifuges used in these plant. For this they used the windows operating system to spread the virus.                                                                 | 2010 | Virus    |
| [[Havex]]                                                          | They focused on industrial control systems with an additional focus on SCADA-control units. The goal was to monitor the information flow and find vulnerabilities. To spread the malware they used the watering-hole-attack.                                                        | 2014 | Malware  |
| [[Dragonfly]]                                                      | Their focus was on industrial control systems and SCADA to leak sensitive information and control these systems.                                                                                                                                                                    | 2017 | Malware  |
| [[Incontroller or PipeDream]]                                      | Specialized for industrial control systems and SCADA and even more in detail on the programmable logic controller and the human machine interface. The malware utilizes the commonly used protocols and disrupts them to harm the smart grid.                                       | 2022 | Malware  |
| [[Trisis or Triton]]                                               | Focuses on the safety instrumented systems of industrial control systems to prevent a given component to send notifications about harmful situations. This attack is different from the others as it directly targets the security and damage prevention systems of the smart grid. | 2017 | Trojaner |
| [[Sunburst]]                                                       | They used a supply-chain attack to get into the network, more precisely they compromised the Orion network management tool and were able to leak sensitive data.                                                                                                                    | 2020 | Malware  |

## A comprehensive Review of Cyberattack on Energy Systems
### Attacks
#### PWM
More common to use energy-limited Pulse Width Modulation jamming signal attacks instead of DoS, as DoS is easy to detect. These attacks use network faults to consume the resources of the system to disable normal operating conditions.

#### DDoS
Distributed Denial of Service (DDoS) have a wider area networking infrastructure for controlling the system. They are harder to detect as they mask themselves through leditimate requests which are scattered over a large number of parties. Thus, it requires background information of interactive features of control devices, physical environment and the communication network to study and defend against such attacks. The detection is simple when they have been executed from an application of a DNS server.

#### False Data Injection Attacks
They differentiate these attacks into multiple ones to be more precise of their mode of operation.

- **Ramp attack**: The ramp FDI attack changes output values of a system or given control signals starting with short time periods of change and increasing these over time until a given maximum is reached.
- **Pulse attack**: In a pulse attack the attacker uses control signals with several attack parameters which are pushed into the system in termporarily distanced short pulses.
- **Random Attack**: These attacks pick the amount of false data or the number of false control signals through a uniformly random function, making them more difficult to predict. 
- **Scaling attack**: This attack follows the general idea of the FDI attack, but adds a scaling parameter, which allows the attacker to scale the amount of false data or false control signals such that she can either reduce her detection chance or increase the impact of her attack.
- **Bias injection attack**: This is the simplest attack of them all as it simply defines a given bias for the attacked sensor or a fix number of control sensor signals which are send repeatedly. 

#### Replay Attacks
This attack is similar to the false data injection attack, but instead of injecting information provided by the attacker this attack monitors a given channel of information and after a certain amount of time replays these signals stopping the other signals that would be send in this time. Thus, it appears to be a legitimate signal that is send while harming the communication.

#### Covert attack
These attacks are sometimes also called masked attacks, where the attacker provides a given attack signal and computes the system output answer, after that she deducts it from the readings of the measurement. Thus, the diagnosis system gets the information measurement without attack data at the controller side, masking/covert the attack. This also works by keeping the attack parameters low enough to stay under the detection system thresholds, allowing the attack to stay hidden while tempering with the data flow.

### Zero dynamics attack
These attacks are not that bis of a concern according to the paper because smart grids are not a least phase system, but the attack in general operates similar to the covert attack. However, the attacker exploits the zero dynamics and linearity of a system transfer function. This allows the attacker to create signals that do not trigger alarms or appear suspicious in the system's output. Furthermore, the attacker does not need access to sensor data but instead execute the attack using an open-loop strategy (without feedback from the system). For this they need two things:
1. Control access to actuators (disrupt ability)
2. Full knowledge of the system's model, particularly the state and output matrices, to calculate the system's zero dynamics.
This attack can be seen as a version of the false data injection attack, but is considered differently in this paper.

### Resonance attack
In power systems, secure and stable operation relies heavily on maintaining acceptable ranges for both frequency and the **Rate of Change of Frequency (RoCoF)**. A **Resonance Attack (ResA)** is a type of cyber-physical attack that manipulates power loads or tie-line signals in a way that **induces abnormal frequency behavior or RoCoF**, using a system’s inherent resonance as the attack vector.

Typically, the **resonance source** is tied to the system’s output function. By carefully adjusting load or tie-line signals to resonate with the system’s dynamics, an attacker can generate subtle, persistent deviations in frequency or RoCoF. These changes are often **small enough to evade conventional detection methods**, particularly if they occur within tolerable time windows.

However, because **RoCoF deviations can eventually lead to frequency instability**, electric grids are configured with **RoCoF Protection Delays (PDs)** to account for inertia and prevent false trips. An attacker exploiting these delays can force RoCoF values to **exceed safe thresholds**, potentially causing **widespread blackouts**.

### Time-Delay switch attack
This attack sets latency in sensors or control loops to reduce system stability. Given a significant delay in remote measurement systems and a time delay that was injected into some equipment or control signals the smart grid will become unstable and can break down. 

### Man-in-the-Middle
As in all other papers this is the most known attack and I wont describe it here again.
