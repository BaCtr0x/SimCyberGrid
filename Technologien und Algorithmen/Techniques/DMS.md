Ein **DMS** (Distribution Management System) ist das Leitsystem, mit dem ein **Verteilnetzbetreiber (DSO)** sein Mittel- und Niederspannungsnetz in Echtzeit überwacht, steuert und optimiert.

### Hauptfunktionen eines DMS
1. **Netzzustandsüberwachung ([[SCADA - Supervisory Control and Data Acquisition|SCADA]]-Layer)**
    - Erfassung von Telemetrie- und Alarmsignalen (Spannung, Strom, Leistung, Gerätestatus) via DNP3, [[IEC 61850]] [[MMS]], [[IEC 60870]]-5-104 etc.
    - Grafische Anzeige von Topologie, Spannungs­profilen und Grenzwertverletzungen.

2. **Lastfluss- und Spannungs­­regelung**    
    - Automatische Berechnung des Netzmodell-Lastflusses (CIM-basiert) alle Sekunden bis Minuten.
    - Volt-VAR-Optimierung (VVO): Setzen von OLTC-Schaltstufen, statischen Kompensatoren, PV-Q-Einspeiseprofilen.

3. **Fehler- und Ausfallmanagement**    
    - **Fault Location, Isolation & Service Restoration (FLISR)**: Automatisierte Isolierung fehlerhafter Netzzonen und Recloser-Sequenzen per IEC 61850-GOOSE oder [[DNP3]]-Control.
    - Outage-Management: Polling von Smart-Meter-Gateways / AMI zur Erkennung unterbrochener Leitungen.

4. **State Estimation & Prognosen**    
    - Schätzen nicht direkt messbarer Zustände (Zweige, Knoten) aufgrund unvollständiger Messdaten.
    - Einspeise- und Lastprognosen (Netzstütz-Profile, Generation Forecast) über Historie und Live-Daten.

5. **Netzschutz-Koordination**    
    - Verteilung von Protection-Parametern (Relay Settings) via IEC 61850-MMS (SPTR, PDIS LN).
    - Abstimmung von Schutzbereichen (“Selectivity”) über Intertripping- und Interlocking-Mechanismen.

6. **Vorgangs- und Alarmmanagement**    
    - Workflow-Steuerung für Einsätze (Dispatch von Reparaturteams).
    - Eskalations- und Benachrichtigungsketten bei kritischen Grenzwertverletzungen.

### Typische Architektur & Schnittstellen
- **Datenquellen**: RTUs, PMUs, SMGWs, AMI, Feldgeräte (IEDs)
- **Kommunikationsprotokolle**: DNP3, IEC 61850 (MMS, GOOSE, SV), IEC 60870-5-104, DLMS/COSEM, OPC UA
- **Datenmodell**: CIM (IEC 61970/61968) für Netzmodell und Topologie
- **Benutzerschnittstelle**: Web- und Desktop-Client mit Kartendarstellung, Alarm- und Reporting-Dashboards
- **Integration**: Schnittstellen zu ERP, GIS, OMS, Network-Planning-Tools

### Abgrenzung zu SCADA
- **SCADA** (Supervisory Control And Data Acquisition) ist der reine Telemetrie- und Steuerungs-Layer.
- **DMS** baut darauf auf und ergänzt erweiterte Netzberechnungen, Automatisierungen und Management-Funktionen.

> **Merksatz:**  
> _Das DMS ist das „Gehirn“ im DSO-Kontrollraum – es verknüpft Mess- und Steuerdaten (SCADA) mit Netzberechnungen, Automatisierungen und Betriebsprozessen, um das Verteilnetz sicher, zuverlässig und effizient zu betreiben._