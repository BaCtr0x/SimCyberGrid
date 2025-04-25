BlackEnergy is a modular malware family that originated around 2007, initially used for DDoS attack and later evolved into a sophisticated espionage and cyber sabotage tool. The third iteration, BalckEnergy 3 (BE3) emerged around 2014 and was stripped down for stealth and exensibility, focusing on persistence, modular payload deployment, and SCADA targeting.

## Architecture
BE3 followed a plugin-based architecture, relying on a small dropper/loader and external plugins for functionality.
1. Dropper/Loader (Initial Vector)
	- A relatively small executable (~40KB)
	- Performs anti-analysis checks (sandbox, debugger detection)
	- Decrypts and loads the core DLL or drops components to disk or memory
2. Plugins/Modules
   These are loaded post-injection and can include:
	- ps.dll: Password stealer (e.g. for Outlook, RDP, browsers)
	- rd.dll: Remote desktop control
	- jn.dll: Keylogger
	- ki.dll: System info enumeration
	- Custom plugins for ICS/SCADA interaction
3. Persistence Mechanism
	- Often achieved through registry run keys, scheduled tasks, or DLL sideloading (common via signed apps like Microsoft Word Viewer)
	- Also used signed drivers to bypass kernel-mode protection in some cases.


## Infection Vectors
The initial access vector for BE3 in the 2015 attack was primarily:
- [[Spear Phishing]] emails with malicious Word documents
	- Contained macros that downloaded the BE3 dropper from a remote C2
	- The macros were often obfuscated with base64 and PowerShell stagers
Once the macro executed:
- It would drop a loader
- The loader would decode and inject the core DLL into a legitimate process (e.g. svchost.exe)

## 2015 Ukraine Power Grid Attack
The BE3 framework was part of a multi-stage attack on three Ukrainian regional power distribution companies
1. Initial Access:
	- Spearphishing delivered BE3 to internal networks
	- Persistent presence was maintained without triggering alarms
2. Lateral Movement & Recon
	- BE3 plugins gathered network topology, credentials and information about ICS/SCADA components
	- Used PsExec, Windows Management Instrumentation (WMI), and somtimes [[Mimikatz]]
3. Payload Execution
	- Custom malware called killDisk was deployed alongside BE3 to:
		- Overwrite boot records or delete files
		- Destroy system executables (including SCADA/HMI software)
	- This was done to impair recovery efforts
4. manual Control of SCADA
	- Attackers remotely logged into HMI workstations (via RDP/VNC)
	- Manually opened breakers in substations via SCADA control interfaces
	- Reports suggest ~30 substations were taken offline, impacting ~225 000 people
5. Communications Disruption
	- Telephony systems (e.g. VoIP call centers) were also disrupted using telephony DoS attacks to prevent customer reporting
	- UPS systems and serial-to-Ethernet converter were bricked
