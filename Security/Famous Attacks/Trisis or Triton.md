Triton discovered in late 2017 and targeted Schneider Eletric Triconex Sagety Instrumented System (SIS) to modify or disable safety logic - potentially to allow unsafe industrial conditions to go unnoticed. 

## What is a Safety Instrumented System (SIS)
In critical infrastrucutre the SIS is separate from the main control system (DCS/PLC). Its only job is to:
- Monitor dangerous conditions (e.g. high pressure, temperature)
- Trigger automatic shutdowns or fail-safes when thresholds are exceeded
So if you disable or subvert the SIS, you can allow unsafe conditions to continue - and potentially cause an explosion or environmental disaster.
Triconex SIS (targeted by TRISIS) uses Triple Modular Redundancy (TMR) and is programmed via a tool called TriStation 1131.

## Technical Architecture of TRISIS
TRISIS was a Python-based remote access trojan bundled with payloads that directly interfaced with SIS logic using Schneider's proprietary protocols.

|Component|Function|
|---|---|
|`Trilog.exe`|Main malware (Python wrapped into executable)|
|`inject.bin`|Malicious safety logic payload to upload to SIS|
|`tsbase.dll`|Reverse-engineered TriStation communication library|
|Logging modules|Wrote to `crashlog.txt`, `error.log` etc. for debugging|

## Attack Flow
### 1. Initial Access (IT to OT)
The attackers were already inside the victim's OT network - via phishing, RDP, VPN, or supply chain.
- They gained access to Windows engineering workstations used to program Triconex SIS via TriStation software.

### 2. Execution of Trilog Malware
- The `Trilog.exe` malware was Python-based, compiled with py2exe
- When run, it:
	- Loaded a custom DLL (`tsbase.dll`) to speak to TriStation protocol
	- Scanned the network for Triconex SIS controllers
	- Pulled the current logic from the SIS
	- Logged detailed system metadata (e.g. controller firmware, configuration)

### 3. Payload Injection to SIS
- Once it identified a target controller, it uploaded `inject.bin` (malicious logic)
- The payload altered the safety logic, possibly to:
	- Suppress shutdowns
	- Introduce logic bombs
	- allow sabotage attempts from the main control system to go unnoticed

### 4. Unintended Crash & Discovery
- The attackers made an error in the payload
-  The controller entered fail-safe mode (shutdown)
- Plant operators found unexpected SIS faults
- an investigation uncovered malware communicating with the SIS over TriStation, leading to the discovery of TRISIS

## How TRISIS Worked (Under the Hood)
- TriStation protocol is proprietary, undocumented and used via serial or Ethernet
- The attackers had:
	- Reversed the protocol
	- Build a working client (in Python)
	- Developed payloads to modify SIS logic
- TRISIS could:
	- Read and write to SIS memory
	- Upload new ladder logic
	- Persist across reboots if flashed

## What Made It So Dangerous?
|Threat Vector|Risk|
|---|---|
|**Targets Safety Layer**|Not just process control, but the system that **protects human lives**|
|**Logic Injection**|Could enable silent sabotage (e.g., let pressure build unnoticed)|
|**Hard to Detect**|Uses **authorized protocols**, signed firmware|
|**Custom Payloads**|Required **intimate understanding of SIS internals**|
|**Nation-State-Level Capability**|Likely custom-built in a **lab environment with real SIS hardware**|
## Why It Failed
- Logic bug caused a crash, triggering plant shutdown
- Altered defenders and prompted deep forensic analysis
- Without that crash, the SIS could have operated with compromised logic, undetected

## Detection & Mitigation
|Layer|Defense|
|---|---|
|**Network**|Monitor for TriStation protocol use over TCP/UDP|
|**Host**|Look for use of `py2exe` payloads; TriStation software anomalies|
|**Access Control**|Limit engineering workstation access (MFA, segmentation)|
|**Integrity Checks**|Use firmware and logic checksums on SIS devices|
|**OT Incident Response**|Have baseline logic backups, and tools to diff logic changes|
