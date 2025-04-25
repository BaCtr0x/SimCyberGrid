Dragonfly and Dragonfly 2.0 are major campaigns tied to state-sponsored cyber-espionage groups targeting energy  and industrial sectors, particularly in the U.S. and Europe. These operations are best known for their multi-stage, stealthy intrusions into ICS/[[SCADA - Supervisory Control and Data Acquisition|SCADA]] networks, with a mix of reconnaissance, credential harvesting and potential staging for sabotage.

## Dragonfly (2011 - 2014)
### Objective 
- Espionage and strategic access into energy and manufacturing infrastructure
- No evidence of sabotage - focus was on network mapping, asset discovery and long-term persistence

### Attribution
- Believes to be Energetic Bear / Crouching Yeti, linked to Russian state actors
- Possibly affiliated with FSB or a military-intelligence contractor

### Techniques Used in Dragonfly
#### 1. [[Spear Phishing]]
- Emails with malicious PDFs or Word docs
- Dropped remote access trojans (RATs) like [[Havex]]

#### 2. Watering Hole Attacks
- Infected websites of ICS software vendors
- Visitors from target companies unknowingly received exploit kits (e.g. LightsOut)

#### 3. Supply Chain Compromise
- Torajanized legitimate ICS software packages (e.g. SCADA drivers, HMI installers)
- Users who downloaded software from vendor websites got infected with Havex

### Havex (Dragonfly's Primary Malware)
- Modular backdoor with plugins:
	- [[OPC - Open Platform Communication|OPC]] scanner: collected ICS tag info
	- Credential stealer
	- Network enumerator
- Communicated over HTTP/S-based C2 channels
- Used legitimate OPC APIs to gather process-level-data - e.g. [[PLC - Programmable Logic Controller|PLC]] tag names, telemetry values

## Dragonfly 2.0 (2015-2017)
### Key Evolution
Dragonfly 2.0 showed a shift from reconnaissance to potential operational disruption - attackers gained access to systems that could control real-world processes.

### Techniques in Dragonfly 2.0
#### 1. Credential Harvesting & Reuse
- Used custom phishing sites and malware (e.g. DropShot, Turtle)
- Collected:
	- VPN credentials
	- Windows credentials
	- Remote access tokens

#### 2. Living of the Land
- Used legitimate admin tools:
	- PowerShell
	- PsExec
	- WMI
- Avoided detection by minimizing custom malware usage

#### 3. Targeting HMI and SCADA Workstations
- Actively accessed systems that:
	- Controlled turbines, breakers, and generators
	- Ran SCADA or HMI software (e.g. GE Cimplicity)
- Screenshot and document collection suggested an operational readiness phase (i.e. preparing for potential kinetic impact)

### Attack Flow in Dragonfly 2.0
1. Initial Access via phishing and credential reuse
2. Lateral Movement into OT environments (via VPNs, weak segmentation)
3. Targeted HMI/SCADA machines
	- Identified software used (WinCC, Cimplicity, etc.)
	- Collected screenshots and config files
4. Maintained persistence and beaconed out via encrypted HTTP(S)

### Malware Used:
| Malware                   | Purpose                                     |
| ------------------------- | ------------------------------------------- |
| **DropShot**              | Loader for secondary payloads               |
| **Turtle**                | Credential harvester                        |
| **Karagany**              | RAT used in earlier campaigns               |
| [[Havex\|Havex (legacy)]] | Still used in some systems for OPC scanning |

### What Made Dragonfly 2.0 Concerning?
- The group demonstrated access to HMI/SCADA interfaces
- Had the technical capacity to manipulate real-world equipment
- Showed long-term persistence
-  Chose not to execute destructive payloads, suggesting strategic restraint - or waiting

### Detection & Defense
| Layer                     | Action                                                                      |
| ------------------------- | --------------------------------------------------------------------------- |
| **Email Filtering**       | Block phishing attempts, scan attachments for known IOCs                    |
| **Software Integrity**    | Verify hashes/signatures of ICS software downloads                          |
| **Network Segmentation**  | Isolate OT systems from IT and external access                              |
| **Behavioral Monitoring** | Look for lateral movement via PsExec, RDP, SMB, unusual OPC browsing        |
| **ICS Anomaly Detection** | Monitor HMI interaction patterns, unauthorized tag access, config downloads |

