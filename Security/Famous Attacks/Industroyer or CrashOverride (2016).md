Discovered after the 2016 Kyiv power outage, this was a purpose-built malware framework designed specifically to control and manipulate industrial protocols - a major escalation.

## Architecture
Industroyer has a modular structure, similar to a nation-state offensive toolkit. 
- The backbone was the loader and orchestrator, which enabled the launcher modules to deploy payloads and handle C2
- These payloads were implemented for industrial control protocols and supported wiper modules, which destroyed registry, corrupts ICS apps (like [[KillDisk]]-lite)
- Lastly the added a Denial-of-Service module to exploit Simens SIPROTEC DoS vulnerability

## Protocol-specific Payloads
Each module implemented legitimate ICS protocols, allowing direct control over substations

| Protocol                | Used For                             | Industroyer Module                   |
| ----------------------- | ------------------------------------ | ------------------------------------ |
| **IEC 60870-5-101/104** | Remote telemetry (Europe, Asia)      | Implemented as TCP client            |
| **IEC 61850**           | Substation automation (modern SCADA) | Parses XML configs, maps to controls |
| **OPC Data Access**     | Windows-based SCADA control          | COM interface for tag manipulation   |
| **[[Modbus]]**          | Legacy devices (rare in this case)   | Used for low-level coil/data control |

## Functionality
- Scans substation networks, identifies endpoints, then issues legitimate control commands
- Could open breakers, change setpoints, or disable protection relays
- Executed at night (~midnight) to reduce immediate detection
- Wiper module would destroy registry and ICS application data after execution

## SIPROTEC DoS Exploit
- Industroyer had a zero-day or N-day exploit against Simens SIPROTEC relays
- Sent a malformed packet over IEC 104 to crash the relay's communication stack
- Result: Protection relays became unresponsive until manually rebooted

