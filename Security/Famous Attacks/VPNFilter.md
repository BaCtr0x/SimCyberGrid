The VPNFilter is a sophisticated, mulit-stage malware that specifically targets network devices such as:
- Home and small office routers
-  Network-attached storage (NAS) device
It was discovered in 2018 and is believed to be created by a state-sponsored group (attributed to the Russian APT group Sofacy/Fancy Bear).

## How It Works - The Three Stages
### 1. Persistence & Loader
- Installs on the router and survives reboots
- Its main job is to download and execute Stage 2.
- It doesn't do anything visibly malicious by itself.

### 2. Core Maleware
- Performs the main malicious activities, including:
	- Data exfiltration
	- Command execution
	- Device manipulation
	- Sniffing and credentials
- It can also brick (destroy) the device on command.

### 3. Plugins (Optional Enhacements)
- Adds extra capabilities like:
	- Packet sniffing
	- [[Modbus]] SCADA protocol targeting
	- Intercepting traffic
	- Routing data through the infected device

## Key Capabilities
- Man-in-the-Middle (MitM) attacks
- Credential harvesting
- Targeted industrial control systems (vis Modbus plugin)
- Encrypted communication with its command-and-control servers
- Destructive "kill switch" that can wipe the device's firmware


### Impact
- Over 500 000 devices were believed to be infected globally.
- Targets included home users, businesses, and critical infrastructure
- FBI and international agencies intervened and seized the command-and-control domain.

