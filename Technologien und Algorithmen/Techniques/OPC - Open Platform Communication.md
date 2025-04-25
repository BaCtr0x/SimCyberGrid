OPC is a middleware standard for data exchange in industrial systems - it lets software like HMIs, historians, and MES systems talk to [[PLC - Programmable Logic Controller|PLCs]].

## How it Works
1. PLC exposes data (via [[Modbus]], Pofinet, etc.)
2. OPC server reads it and maps variables to tags
3. Client apps (HMI, SCADA historian) subscribe to tags for real-time updates

## In the Context of Attacks
- [[Stuxnet]] modified **PLC logic**
- [[Trisis or Triton]] injected malicious logic into a **safety PLC**
- [[Havex]] scanned **OPC servers** to enumerate **OPC tags**, letting attackers **map out the industrial process** remotely
- [[Industroyer or CrashOverride (2016)]] used legitimate protocols (like IEC 104, OPC DA) to **interact with devices via their tags**