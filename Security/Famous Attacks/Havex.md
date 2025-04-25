Havex is one of the earlier but highly significant pieces of ICS-focused malware, notable for its role in industrial espionage and its use of software supply chain compromise, years before it became a hot topic post-[[Sunburst|Solarburst/SolarWinds]].

## Overview
- Discovered in 2013-2014
- Threat Actor: Energetic Bear / Dragonfly (suspected Russian APT)
- Primary Purpose: Cyber espionage - data collection, network mapping, asset discovery
- Unique Feature: included a module to scan and fingerprint industrial control systems, particularly using OPC (OLE for Process Control)

## Targets
- Energy sector
- Manufacturing
- Pharmaceuticals
- Water utilities
- Regions: Europe and North America

## Malware Architecture
Havex was modular - its core backdoor could load a variety of plugins for different tasks.

### Core Components
| Component                        | Purpose                                                          |
| -------------------------------- | ---------------------------------------------------------------- |
| **Main backdoor (Havex RAT)**    | Initial access, command and control (C2), and plugin loader      |
| **OPC scanner module**           | ICS-specific — scanned for OPC DA servers and gathered tag info  |
| **Credential harvesting plugin** | Extracted credentials from memory, registry, config files        |
| **File system scanner**          | Looked for specific file types (e.g., engineering project files) |
| **Network scanner**              | Enumerated devices and open ports on internal networks           |

## Initial Infection Vectors
Havex was distributed through three main techniques, one of which is especially noteworthy:
### 1. Water Hole Attacks
- Compromised legitimate websites of industrial or energy companies
- Injected malicious iframe or JavaScript redirect victims to exploit kits (like LightsOut)
- Delivered Havex as a payload

### 2. Phishing Emails
- Malicious attachments or links
- Used basic downloaders to drop the Havex core

### 3. Software Supply Chain Compromise
- Attackers compromised ICS vendor websites
- Trojans were injected into legitimate software installers
-  Examples: Trojanized versions of ICS device drivers or programming tools
- When customers downloaded and installed the tools, they inadvertently installed Havex

This meant companies trusted the software and introduced the malware with admin privileges into ICS/OT environments.

## OPC Scanner Module - ICS-Specific Payload
This is the most important and novel part of Havex from an ICS perspective
### What it Did:
#### 1. Scanned the local network for:
- OPC servers
- Open DCOM interfaces
- Specific ports (135, 445)
#### 2. Connected to OPC DA (Data Access) servers
- Using standard DCOM/COM interfaces
- Called legitimate OPC APIs to:
	- Enumerate tags (e.g. `TemperatureSensor01`)
	- Dump tag values, data types, and timestamps
#### 3. Sent dat aback to C2
- Allowed adversaries to map out ICS process variables
- Enabled follow-up operations or future sabotage planning

OPC is widely used in legacy ICS environments as middlemare between PLCs, HMIs and SCADA systems. By scanning the OPC tags, Havex essentially did industrial reconnaissance.


## Command & Control (C2)
- Communicated over HTTP(S)
- Used base64-encoded payloads
- In some variants, used custom C2 protocols or hidden tunnels
- C2 domains often mimicked vendor names or legitimate services

## Sample Tactics in the Wild
One Havex sample contained a plugin that:
- Found OPC DA server at `MACHINE_A`
- Enumerated ~700 tag names (e.g. `PUMP_01_Speed`, `TEMP_VALVE3`)
- Exfiltrated:
	- Tag list
	- Tag values
	- OPC server names and versions
This allowed attackers to build detailed knowledge of the physical process - what assets were there, how they were names, what vlalues they operated at.

## Strategic Goal
Haves was not destructive. Its goal was:
- Long-term espionage
- Industrial system profiling
- Possibly laying the groundwork for future disruption

Think of it like recon + foothold, not kinetic sabotage like [[Stuxnet]] or [[Trisis or Triton]]

## Detection & Indicatos
### IOC Examples:
- OPC-related COM interface usage from non-engineering systems
- HTTP POSTs to C2 domains (with Base64 payloads)
- Trojanized ICS software hashes
- DLLs loaded into `opc.exe`, `opcdasrv.exe` or similar

### Defensive Techniques:
| Control                        | Description                                                 |
| ------------------------------ | ----------------------------------------------------------- |
| **Network Segmentation**       | Separate IT/OT networks — Havex spreads laterally           |
| **Executable Whitelisting**    | Block unauthorized COM/DCOM clients from accessing OPC      |
| **Download Authenticity**      | Hash-check ICS tools; verify against vendor-signed versions |
| **ICS-aware Threat Detection** | Monitor for unusual OPC tag enumeration                     |