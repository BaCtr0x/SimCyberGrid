Incontroller/PipeDream is one of the most dangerous pieces of ICS/OT malware ever discovered, on par with Stuxnet and Triton. it was revealed in April 2022 and is attributed to a nation-state-level actor, likely with capabilities for kinetic disruption of critical infrastructure. 

## What is Incontroller/PipeDream
- Type: ICS/SCADA malware framework
- First disclosed: April 13, 2022 (Dragos/Mandiant)
- Targeted Systems:
	- Schneider Electric programable logic controllers (PLC)s (Modicon)
	- Omron PLCs (NX/NJ)
	- Open Platform Communication unified architecture (OPC UA) servers
- Purpose: Enable attackers to reprogram, control, and disrupt physical processes in sectors like power, water, oil/gas

Unlike Stuxnet (very targeted), PipeDream was designed to be modular and reusable across environments - a potential ICS cyber weapon platform.

## High-Level Architecture
PipeDream consists of multiple components that interact with industrial control systems using legitimate protocols:

| Component             | Purpose                                                              |
| --------------------- | -------------------------------------------------------------------- |
| `CodeSys` module      | Exploits vulnerabilities in devices using CodeSys automation runtime |
| `OMRON` module        | Communicates directly with Omron PLCs (via FINS protocol)            |
| `MODBUS` module       | Targets Schneider Electric Modicon PLCs using [[Modbus]] TCP         |
| `OPC UA` module       | Interfaces with industrial middleware and telemetry systems          |
| `Tagrun` tool         | Custom payload executor on Windows systems                           |
| `Owlproxy`            | Covert tunneling tool; possibly SOCKS5 proxy                         |
| `Mousejacking` module | Attacks human-machine interfaces (HMI) via wireless input spoofing   |

each module uses native, vendor-specific communication protocols to interact with PLCs and SCADA devices without exploits. Some modules do contain known or suspected 0-days.

## Attack Flow
### 1. Initial Access
Not part of PipeDream itself - assumes the attacker has already gained access via IT/Ot breach, phishing, WPN exploit, etc.

### 2. Discovery & Recon
- Use of tools to identify:
	- PLC vencors Schneider, Omron
	- OPC UA endpoints
	- Network layout and segmentation

## 3. Stage 1 - Protocol Exploitation and Access
#### CodeSys Module
- Uses CodeSys v3 protocol to:
	- Upload malicious logic
	- Start/stop PLC processes
	- Alter program execution
- Likely includes:
	- Unauthenticated or weakly authenticated commands
	-  Exployits to bypass memory protections

#### Modbus TCP Module (SchneiderElectric)
- Issues valid Modbus commands:
	- Coil write (`0x05`)
	- Register write (`0x06`)
	- Force stop/start
	- Reconfigure safety settings
- Can brick or put PLCs in fault states

#### OMRON Module
- Uses FINS protocol:
	- Uploads ladder logic or function blocks
	- Start/stops CPU
	- Reads I/O memory
	- Issues warm/cold restarts

### 4. Stage 2 - Persistence & Payload Execution
#### Tagrun
- Executes malicious scripts on Windows-based engineering workstations
- Supports payloads like:
	- Data collection
	- Logic tampering
	- Operator interface manipulation

#### Owlproxy
- Establishes convert C2 tunnels, potentially over SOCKS5
- Maybe used to route traffic out or air-gapped environments via pivoted devices

### Stage 3 - Attack Execution
At this point the attacker can cause physical disruption or even destruction by interacting directly with field devices.
- Exmaples:
	- Open/close valves or breakers
	- Disable safety systems
	- Introduce erratic behavior in PID loops
	- Overwrite firmware or logic to brick devices

## Unique & Dangerous Capabilities
|Feature|Why It's Dangerous|
|---|---|
|**Vendor-agnostic toolkit**|Supports multiple brands across industries|
|**Protocol-native communication**|No need for exploits — harder to detect|
|**Modular framework**|Reusable by other actors, adaptable for new devices|
|**Custom tunneling (Owlproxy)**|Enables long-term covert presence|
|**Live interaction with PLCs**|Operator-like control over field devices|
|**Mousejacking**|Can manipulate HMIs via spoofed USB dongles/wireless|
## Comparison: PipeDream vs Other ICS Malware
| Malware                                 | Target                   | Primary Method                | Intent                     |
| --------------------------------------- | ------------------------ | ----------------------------- | -------------------------- |
| [[Stuxnet]]                             | Siemens PLCs             | Exploits + payload injection  | Sabotage (centrifuges)     |
| **Triton/Trisis**                       | Schneider SIS            | Remote code injection         | Safety system disablement  |
| [[Industroyer or CrashOverride (2016)]] | Electric substations     | Native protocols              | Grid disruption            |
| **PipeDream/Incontroller**              | Schneider, Omron, OPC UA | Native control + exploitation | Modular disruption toolkit |

## Detection & Defense
### Indicators of PipeDream Use:
- Unusual Modbus/DINS/CodeSys traffic from engineering workstations
- Unauthorized ladder logic changes or CPU reboots
- OPC UA clients issuing mass tag reads/writes
- Abnormal coil write (`0x05`) and register write (`0x06`) sequences
- Use of `codeSysControlService.exe` or `tagrun.exe`

### Defense Strategies:
|Layer|Action|
|---|---|
|**Network Segmentation**|Strict separation of IT/OT; no internet access to engineering workstations|
|**Protocol Whitelisting**|Only allow expected PLC protocols and command types|
|**Deep Packet Inspection**|Monitor for unauthorized Modbus/FINS traffic|
|**Firmware Verification**|Check PLCs for unauthorized code uploads|
|**Asset Hardening**|Disable unused services on PLCs; enforce authentication|