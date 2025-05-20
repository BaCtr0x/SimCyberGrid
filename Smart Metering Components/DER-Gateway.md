Ein **DER-Gateway** (Distributed Energy Resource Gateway) ist die **Kommunikations- und Steuer­schnittstelle** zwischen dezentralen Erzeugungs- bzw. Speicheranlagen (PV-Inverter, Batteriewechselrichter, Biogas-Generatoren etc.) und übergeordneten Steuer- und Markt-Systemen. Seine Hauptaufgaben lassen sich folgendermaßen zusammenfassen:

## 1. Protokoll-Übersetzung & Datenmodellierung

- **Oberflächen-Protokolle**:    
    - **[[IEC 61850]]-[[MMS]]** für lokale Substations-Anwendungen (Logical Nodes wie DERC, DERG, DERF).
    - **[[TR-03109]] CLS** (ControlMessage JSON/XML) für TargetPower- und LoadReduction-Befehle im Smart-Meter-Umfeld.
    - **[[IEEE 2030.5]]** („Smart Energy Profile“) für Prosumer-Kommunikation in Wohngebäuden.
    - **[[OpenADR 2.0b]]** für Demand-Response-Programme (oadrDistributeEvent → VEN).
    - **[[IEC 63110]]** für Bidirektionales Laden (MeterValues, SetChargingProfile).

- **Feld-Protokolle**:    
    - Proprietäre oder herstellerspezifische Inverter-APIs (Modbus-TCP / SunSpec, CAN-Bus, RS-485).
    - OPC UA oder MQTT für neue Industrie-Gateways.


> **Aufwand**: Der Gateway „übersetzt“ also beispielsweise einen OpenADR-Event in einen IEC 61850-Operate(“DERG.Pos.stVal“) oder in ein SunSpec-Modbus-Write, je nach Anlage.


## 2. Telemetrie-Aggregation & Reporting

- **Polling** der angeschlossenen DERs in festen Intervallen (z. B. jede Sekunde die aktuellen P/Q/SOC/Wirkwirkungsgrade).    
- **Event-Reporting** bei Grenzwertverletzungen (Übertemperatur, Überstrom, Netzauf- oder –abtrennungen).
- **Kontextangereicherte InfoReports**:
    - Führen Timestamp (PTP/NTP), Quality-Flags und Geräte-Metadaten mit.
    - Bündeln Messwerte (z. B. PV-Leistung + Batterieladezustand) in einem JSON/MMS-RBD (Report by Data Change).
- **Rückmeldung an Steuerzentralen**:
    - CMS-signierte Telemetrie-Reports via TLS an DMS, VPP-Operator oder µGrid-Controller.
    - Bei Nutzung von IEEE 2030.5 oder IEC 63110 direkt an das Cloud-Backend oder Prosumer-Portal.


## 3. Steuer- und Regelbefehle

- **Setpoints verarbeiten**:    
    - Empfang von CLS-ControlMessages oder MMS-Operate-Requests.
    - Übersetzen in herstellerspezifische Steuerbefehle (z. B. Modbus-Holding-Register, REST-API-Calls).
- **Acknowledge-Logik**:
    - Nach BSI-TR-03109-5 → Gateway-ACK als JSON über HTTPS oder MMS-Response.
    - Bei IEC 61850 → Select/Operate-Bestätigung (SelectResponse, OperateResponse).
    - Timeout-Überwachung & Retransmit (z. B. ACK ≤ 1 s, sonst erneutes Senden bis 3 ×).
- **Lokale Absicherung**:
    - Schaltstellen sind auf Fallback-Logiken programmiert (z. B. lokale Unterspannungsauslösung), falls der Gateway einmal nicht erreichbar ist.


## 4. Sicherheit & Zertifikatsmanagement

- **TLS-1.2/1.3** mit mutual [[X.509]]-Zertifikat­authentisierung (SM-PKI oder eigene PKI der Versorger).    
- **CMS-Signaturen** auf allen ControlMessages und Telemetrie-Reports.
- **Zertifikats-Rollout**: OCSP-Checks oder CRL-Prüfung vor jeder neuen Verbindung; Key-Roll-Over via [[IEC 62351]]-6.
- **HSM-Anbindung** (PKCS#11) für sicheren Schutz privater Schlüssel und schnelle Signatur­prozesse.


## 5. Edge-Intelligenz & Resilienz

- **Offline-Betrieb**: Bei Netzverlust puffert der Gateway zuletzt empfangene Setpoints und führt sie bei Wiederkehr selbstständig aus.    
- **Regelalgorithmen on-board**: Lokale Volt-VAR-Optimierung oder einfache droop-basierte Frequenzregler, um Stabilität auch ohne zentralen Befehl zu gewährleisten.
- **Fehler-Überwachung**:
    - Watchdog-Funktion für Kommunikations- und Geräte-Health.
    - Automatische Neustarts und Fallback-Modi bei Hangs/Fehlfunktionen.


## 6. Schnittstellen zu anderen Systemen

- **REST/WebSocket APIs** für Management- und Reporting-Tools.    
- **MQTT** oder **AMQP** für skalierbare Cloud-Anbindung.
- **OPC UA** für industrielle Integrations-Use-Cases.


> **Kurz gefasst:**  
> Das DER-Gateway ist **Dolmetscher**, **Sicherungspuffer**, **lokaler Regler** und **Schlüsseldrehscheibe** zwischen Feldgerät und Cloud/Leitstelle: Es empfängt vielfältige zentrale Setpoints, übersetzt sie in Gerätebefehle, sammelt Telemetrie, versieht alles mit Sicherheit (TLS/CMS) und stellt es den übergeordneten Systemen wieder in normierten Protokollen und Formaten bereit.