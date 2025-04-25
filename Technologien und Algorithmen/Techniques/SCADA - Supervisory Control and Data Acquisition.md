SCADA is a system architecture used to remotely monitor, control and collect data from industrial preocesses. it connects field devices ([[PLC - Programmable Logic Controller|PLCs]], sensors) to human operators and centralized systems.

It's like the nervous system of industrial automation - it collects, transmits, visualizes and controls industrial data and processes from one or more sites. 

## SCADA System Components
|Component|Role|
|---|---|
|**Field Devices**|Sensors, actuators, and PLCs that interact with the physical process|
|**RTUs / PLCs**|Collect sensor data and execute control logic|
|**Communication Infrastructure**|Transmits data from remote sites to central control (wired, RF, cellular, satellite)|
|**SCADA Master Server / Data Server**|Collects data from devices, logs events, manages alarms|
|**HMI (Human-Machine Interface)**|GUI used by operators to visualize and control the system|
|**Historian**|Stores time-series data (temperatures, pressures, system states) for analysis|

## How SCADA Works (Conceptual Flow)
1. Sensors detect real-world parameters (e.g. flow rate, pressure)
2. PLCs/RTUs read sensor input and execute control logic
3. SCADA Server collects data from PLCs via protocols ([[Modbus]], DNP3, [[OPC - Open Platform Communication|OPC]], IEC 104, etc.)
4. Human machine interface (HMI) displays real-time data for operators
5. Operators can send commands (e.g. "open valve", "shut down pump") through HMI
6. All data end events are logged for auditing and analysis

## SCADA vs DCS
|Feature|SCADA|DCS (Distributed Control System)|
|---|---|---|
|**Focus**|Supervisory & remote monitoring|Localized real-time control|
|**Scale**|Geographically distributed|Plant/factory-level|
|**Network Type**|Long-distance (WAN, radio, etc.)|Local (LAN)|
|**Examples**|Water utilities, power grids|Chemical plants, refineries|
## in Cybersecurity Context
### Why SCADA is a High-Value Target
- Often controls critical infrastructure
- May include legacy systems with no encryption/authentication
- Often connected to IT networks for analytics, exposing it to external threats

### Notable SCADA/Targeting Malware:
| Malware                                 | Role                                                           |
| --------------------------------------- | -------------------------------------------------------------- |
| [[Stuxnet]]                             | Attacked Siemens SCADA via PLC logic injection                 |
| [[Industroyer or CrashOverride (2016)]] | Sent protocol-level commands to substation SCADA systems       |
| [[Havex]]                               | Enumerated OPC tags in SCADA networks                          |
| [[Trisis or Triton]]                    | Attacked safety controllers often managed via SCADA interfaces |
