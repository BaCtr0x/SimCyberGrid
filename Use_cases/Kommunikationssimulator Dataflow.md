
## Komponenten

| Komponenten                    | Beschreibung                                                                                                             |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| CRL-Distribution Server        | Stellt Certificate Revocation List (CRLs) bereit, damit Clients Zertifikats gueltigkeit pruefen koennen.                 |
| DER-Gateway                    | Schnittstelle zu dezentralen Erzeugungs- bzw. Speicheranlagen fuer Setpoints (P/Q) und Telemetrie (ACK, Status)          |
| DSO-DMS                        | Distribution Management System: Netzueberwachung, Lastfluss- und Spannungsregelung, FLISR-Funktionen                     |
| EVSE-Gateway                   | Schnittstelle zu Ladestationen: V2G-Setpoints (ISO 15118), Messwerte ([[IEC 63110]]) und Lade-ACKs                       |
| IDS/SIEM (SOC)                 | Empfaengt IDS-Alarme via Syslog, korreliert Security-Events und priorisiert Vorfaelle fuer das Security Operation Center |
| Microgrid-Controller           | Bedienoberflaeche und Steuerungfseben fuer grid-connected Microgrids; zeigt MMS-Reports und sendet Dispatch-Befehle      |
| Netz-Simulator                 | Erzeugt synthetische Netzzustandsdaten (Spannung, Strom, Pahsoren) und Fehlerscenarien fuer die Co-Simulation            |
| OCSP-Responder                 | On-Line Certificate Status Protocol: gibt in Echtzeit den Wiederrufstatus von [[X.509]]-Zertifikaten aus.                |
| Operational Data Store (ODS)   | Data Warehouse/Clearinghouse: Batch-Transfer anonymisierte Meter-Readings und historischer Datensaetze                   |
| OperatorUI                     | Dies ist das Grid-Operator-Dashboard, wodurch der Operator mit dem System interagieren kann.                             |
| Outage management System (OMS) | System fuer Ausfallermittlung: Polling von Smart Meter Gateways (ANSI C12.22/DLMS) und Auswerten von Responses           |
| PMU (Phasor Measurement Unit)  | Messen von Phasorgroessen (U/I, Frequenz, ROCOF) mit PTP-Zeitstempel und Streaming an WAMS                               |
| Protection-IED                 | Schutzrelais fuer Distanzschutz, Differentialschutz, trippt und isoliert fehlerhafte Netzzonen via GOOSE                 |
| Smart Meter Gateway (SMGW)     | Erfasst Zaehlerdaten, verpackt sie als InfoReports und steuert ueber ControlMessages Hausanschlussgeraete                |
| VNB-SCADA / VNB-Backend        | Leitsystem des Verteilnetzbetreibers fuer Smart-Meter-Daten und CLS-Steuerung (Load-/Generation-Commands)                |
| VPP-Operator                   | Virtuelles Kraftwerks-Management: Registrierung/Deregistrierung, Aggergation von Forecasts und Schedules                 |
| WAMS-Backend / PDC             | Phasordaten-Konzentrator und Analyseplattform fuer Wide-Area Monitoring & Protection (WAMPAC, State Estimation)          |


## Kommunikation

| Komoponente               | Kommuniziert mit                                                | Datentyp/Nachricht                                                                                                                   | Protokoll/Schema                                                                                                                                       |
| ------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Smart Meter Gateway       | VNB-[[SCADA - Supervisory Control and Data Acquisition\|SCADA]] | $\rightarrow$ InfoReport (TAC-Container)<br>$\leftarrow$ Control Message (TargetPower / LoadReduction)                               | $\rightarrow$ HTTPS/TLS 1.2+ mit CMS-signiertem JSON/XML (FNN-XSD/JSON-Schema)<br>$\leftarrow$ HTTPS/TLS 1.2+ mit CMS-signiertem CLS-JSON (TR-03109-5) |
| Smart Meter Gateway       | [[Distribution System Operator\|DSO]]-[[DMS]]                   | $\rightarrow$ Aggregierte InforReports                                                                                               | $\rightarrow$ HTTPS/TLS1.2+ mit CIM-XML ([[IEC 61970]]-9)                                                                                              |
| DSO-DMS                   | [[DER-Gateway]]                                                 | $\rightarrow$ CLS-Setpoint (TargetPower / LoadReduction)<br>$\leftarrow$ Gateway-ACK (ControlAck)                                    | $\rightarrow$ HTTPS/TLS 1.2+ mit CMS-signiertem CLS-JSON (TR-03109-5)<br>$\leftarrow$ HTTPS/TLS 1.2+ mit einfachem JSON                                |
| PMU                       | [[WAMS]]-Backend                                                | $\rightarrow$ Synchrophasor Data Frame<br>$\leftarrow$ Command Frame (Control Frame)                                                 | $\rightarrow$ [[IEC 61850]]-90-5 over UDP/IP + TLS ([[IEC 62351]]-5), IEEE C37.118.2<br>$\leftarrow$ IEC 61850-90-5 over UDP/IP + TLS                  |
| DSO-DMS                   | Protection-IED                                                  | $\rightarrow$ [[GOOSE]] Trip/Operate Frames<br>$\leftarrow$ GOOSE Confirmation                                                       | $\rightarrow$ IEC 61850-GOOSE TLS-getunnel (IEC 62351-6)<br>$\leftarrow$ IEC 61850-GOOSE                                                               |
| VPP-Operator              | DERGateway                                                      | $\rightarrow$ RegisterDer / DeregisterDER<br>$\leftarrow$ EntrollAck                                                                 | $\rightarrow$ HTTPS/TLS 1.2+ mit CMS-signiertem IEC 63110 DeviceProvisioning<br>$\leftarrow$ HTTPS/TLS 1.2+ mit einfachem JSON                         |
| VPP-Operator              | DERGateway                                                      | $\rightarrow$ ScheduleMessage (Day-Ahead / Forecast)<br>$\leftarrow$ Telemetrie (DERTelemetry)                                       | $\rightarrow$ AS4/ebMS3 over HTTPS/TLS 1.2+ mit CMS-signiertem CIM-XML<br>$\leftarrow$ HTTPS/TLS 1.2+ mit CMS-signiertem JSON ([[IEEE 2030.5]])        |
| $\mu$Grid-Controller / UI | DER-Gateway                                                     | $\rightarrow$ [[IEC 61850]]-[[MMS]] Reports (1 s-Raster)<br>$\leftarrow$ Control (Operate, TargetPower)                              | $\rightarrow$ MMS over TCP/TLS (IEC 62351-3)<br>$\leftarrow$ MMS/TLS oder CLS-JSON                                                                     |
| $\mu$Grid-Controller / UI | EVSE-Gateway                                                    | $\rightarrow$ SetChargingProfile<br>$\leftarrow$ MeterValues (P/Q, SOC)                                                              | $\rightarrow$ ISO 15118-20 ‘ScheduleExchange’ over TLS 1.3<br>$\leftarrow$ IEC 63110 ‘MeterValues’ over TLS                                            |
| Smart Meter Gateway       | Operational Data Store                                          | $\rightarrow$ MeterReading Batches                                                                                                   | $\rightarrow$ SFTP/TLS 1.3 oder HTTPS/TLS 1.3 + CIM-XML / GreenButton JSON                                                                             |
| Smart Meter Gateway       | Outage Management System                                        | $\rightarrow$ PowerStatusPoll<br>$\leftarrow$ PollResponse (Outage-Status)                                                           | $\rightarrow$ ANSI C12.22 / [[DLMS]]-[[COSEM]] over TLS<br>$\leftarrow$ ANSI C12.22 / DLMS-COSEM over TLS                                              |
| Smart Meter Gateway       | OCSP-Responder                                                  | $\rightarrow$ OCSP Request<br>$\leftarrow$ OCSP Response                                                                             | $\rightarrow$ HTTP(S)<br>$\leftarrow$ HTTP(S)                                                                                                          |
| Smart Meter Gateway       | CRL-Distribution Server                                         | $\rightarrow$ CRL Download                                                                                                           | $\rightarrow$ HTTP(S)                                                                                                                                  |
| Smart Meter Gateway       | IDS/SIEM (SOC)                                                  | $\rightarrow$ IDS-Syslog Alarme                                                                                                      | $\rightarrow$ Syslog ([[RFC 5424]]) over TLS ([[RFC 5425]])                                                                                            |
| WAMS-Backend              | OperatorUI                                                      | $\rightarrow$ Live Phasor-Dashboard-Data                                                                                             | $\rightarrow$ WebSocket/TLS mit JSON (custom-Schema)                                                                                                   |
| DSO-DMS                   | OperatorUI                                                      | $\rightarrow$ SCADA Telemetrie (Spannung, Strom, Alarme, Status)<br>$\leftarrow$ Manuelle Steuerbefehle (Swtich, Setpoints, Reclose) | $\rightarrow$ ICE 61850 MMS Report (CIM-XML over TLS)<br>$\leftarrow$ IEC 61850 MMS Operate/SetDataValues over TLS                                     |
| WAMS-Backend              | DSO-DMS                                                         | $\rightarrow$ PhasorReports                                                                                                          | $\rightarrow$ IEC 61850 MMS Report (CIM-XML over TLS)                                                                                                  |

```mermaid
---
title: Dataflow Diagram Communication Simulator
---
flowchart LR

  subgraph Metering_Settlement
    style Metering_Settlement fill:#fdf6e3,stroke:#eee,stroke-width:1px
    SMGW([SMGW])
    VNBSCADA([VNB-SCADA])
    OMS([Outage Mgmt System])
    ODS([Operational Data Store])
  end

  subgraph Distribution_Management
    style Distribution_Management fill:#e8f6f3,stroke:#eee,stroke-width:1px
    DSODMS([DSO-DMS])
    IED([Protection-IED])
    OperatorUI([Operator UI])
  end

  subgraph DER_VPP
    style DER_VPP fill:#f3e8f6,stroke:#eee,stroke-width:1px
    DERGW([DER-Gateway])
    VPP([VPP-Operator])
  end

  subgraph Grid_Stability
    style Grid_Stability fill:#e8eefa,stroke:#eee,stroke-width:1px
    PMU([PMU])
    WAMS([WAMS-Backend])
  end

  subgraph Microgrid_EVSE
    style Microgrid_EVSE fill:#eefae8,stroke:#eee,stroke-width:1px
    MC([Microgrid Controller])
    EVSE([EVSE-Gateway])
  end

  subgraph Security_Services
    style Security_Services fill:#f4f4f4,stroke:#ccc,stroke-width:1px,stroke-dasharray: 5 2
    OCSP([OCSP-Responder])
    CRL([CRL-Server])
    IDS([IDS/SIEM])
  end

  %% Verbindungen Metering
  SMGW -->|InfoReport| VNBSCADA
  VNBSCADA -->|ControlMessage| SMGW
  SMGW -->|PowerStatusPoll| OMS
  OMS -->|PollResponse| SMGW
  SMGW -->|MeterReading| ODS

  %% Verbindungen Distribution
  VNBSCADA -->|Agg. Reports| DSODMS
  DSODMS -->|GOOSE Trip| IED
  IED -->|GOOSE Ack| DSODMS
  DSODMS -->|SCADA Telemetrie| OperatorUI
  OperatorUI -->|Manual Operate| DSODMS

  %% Verbindungen DER & VPP
  DSODMS -->|CLS-Setpoint| DERGW
  DERGW -->|ACK/Telem.| DSODMS
  VPP -->|Register/Schedule| DERGW
  DERGW -->|EnrollAck/Telemetry| VPP

  %% Verbindungen Grid Stability
  PMU -->|Data Frame| WAMS
  WAMS -->|Command Frame| PMU
  WAMS -->|Aggreg. Phasors| DSODMS
  WAMS -->|Live Phasor| OperatorUI

  %% Verbindungen Microgrid
  MC -->|MMS Reports| DERGW
  DERGW -->|Operate| MC
  MC -->|SetChProfile| EVSE
  EVSE -->|MeterValues| MC

  %% Verbindungen Security
  SMGW -->|OCSPRequest| OCSP
  OCSP -->|OCSPResponse| SMGW
  SMGW -->|CRLDownload| CRL
  SMGW -->|Syslog| IDS

  %% Style-Definitionen
  linkStyle 5,10,11,16,17,18,19,22,23,24,25 stroke:#ffbb33,stroke-width:2px,color:#ffbb33
  linkStyle 0,1,2,3,4,6,7,8,9,12,13,14,15,20,21 stroke:#86d8f7,stroke-width:2px,color:#86d8f7
```

