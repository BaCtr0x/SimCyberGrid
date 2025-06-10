## Schutzziele
![[Schutzziele#Schutzziele]]
## Assets Based
### Assets
![[Kommunikationssimulator Dataflow#Komponenten]]

![[Kommunikationssimulator Dataflow#Kommunikation]]
## Most vulnerable Assets with Threats
| Asset Category               | Example Components                  | Key Threats/Vulnerabilities                    | Potential Impact                            |
| ---------------------------- | ----------------------------------- | ---------------------------------------------- | ------------------------------------------- |
| Smart Meter Endpoints        | SMGW, Smart Meters                  | Spoofing, remote tripping, botnets, data theft | Outages, privacy loss, grid instability     |
| Control Centers              | DSO-DMS, VNB-SCADA, OMS             | DDoS, command spoofing, ransomware, insiders   | Grid mismanagement, outages, safety risks   |
| Communication Infrastructure | DER-Gateway, EVSE-Gateway, Networks | Interception, false data injection, DoS        | Service disruption, manipulated grid load   |
| Security Infrastructure      | CRL-Server, OCSP, IDS/SIEM          | Crypto attacks, impersonation, DoS             | Loss of trust, undetected breaches          |
| Data Stores                  | ODS, WAMS-Backend/PDC               | Data theft, manipulation, ransomware           | Data loss, compliance issues, trust erosion |

## [[OCTAVE]]
### Likelyhoods
- **Low (rare)**
- **Medium (possible)**
- **High (likely)**

### Impact
- **Low (Minor)**
- **Moderate (significant)**
- **High (Severe)**

### Prioritize and Mitigation Risks
1. **MItigate:** High-likelyhodde/high-impact risks
2. **Mitigate/Defer:** Medium risks
3. **Defer or Accept:** low risks
4. **Accept:** negligible risks


### OCATAVE Table

| Asset                | Area of Concern                       | Threat Scenario                                                   | Impact   | Likelihood | Priority | Mitigation                        |
| -------------------- | ------------------------------------- | ----------------------------------------------------------------- | -------- | ---------- | -------- | --------------------------------- |
| CRL-Server           | Service unavailability                | DoS attack blocks certificate validation                          | High     | Medium     | 1        | Redundancy, monitoring            |
| DER-Gateway          | Setpoint manipulation                 | Attacker injects malicious setpoints                              | High     | Medium     | 1        | Input validation, auth            |
| DSO-DMS              | Compromise of grid commands           | Insider modifies grid parameters                                  | High     | Medium     | 1        | Access control, monitoring        |
| ODS                  | Data breach/manipulation              | Malware exfiltrates/changes data                                  | Moderate | Medium     | 2        | Encryption, access restriction    |
| Protection-IED       | Relay setting modification            | Malicious config changes cause outages                            | High     | Low        | 2        | Config mgmt, monitoring           |
| SMGW                 | Unauthorized access/tampering         | Remote exploit for data/control manipulation                      | High     | High       | 1        | Auth, updates, monitoring         |
| EVSE-Gateway         | Setpoint manipulation                 | Attacker injects malicious setpoints                              | High     | Medium     | 1        | Input validation, auth            |
| IDS/SIEM (SOC)       | Service unavailable, datamanipulation | DoS attack blocks priorization, attacker manipulates priorization | High     | High       | 1        | majority voting, auth, redundancy |
| Microgrid-Controller |                                       |                                                                   |          |            |          |                                   |
| Netz-Simulator       |                                       |                                                                   |          |            |          |                                   |
| OCSP-Responder       |                                       |                                                                   |          |            |          |                                   |
| OperatorUI           |                                       |                                                                   |          |            |          |                                   |
| OMS                  |                                       |                                                                   |          |            |          |                                   |
| PMU                  |                                       |                                                                   |          |            |          |                                   |
| VNB-SCADA            |                                       |                                                                   |          |            |          |                                   |
| VPP-Operator         |                                       |                                                                   |          |            |          |                                   |
| WAMS                 |                                       |                                                                   |          |            |          |                                   |
