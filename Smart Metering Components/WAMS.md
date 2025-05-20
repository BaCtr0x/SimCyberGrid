Ein **WAMS (Wide-Area Measurement System)** übernimmt in modernen Stromnetzen vor allem die **übergreifende Erfassung**, **Aufbereitung** und **Auswertung** von hochaufgelösten Messdaten (Synchrophasoren) aus weit verteilten Netz­punkten, um so eine **netzweite Situations­übersicht** in quasi-Echtzeit zu gewinnen.

### 1. Kernkomponenten

- **Phasor Measurement Units (PMUs)**  
    Erfassen Spannung und Strom als Vektor­größen (Magnitude & Phase), Frequenz und ROCOF mit Abtastraten von 30–60 fps und versehen sie mit präzisen PTP-Zeitstempeln.
- **Phasor Data Concentrator (PDC)**  
    Sammelt die Streams aller PMUs, zeitsynchronisiert sie (Alignment), filtert Ausreißer und speist sie weiter an Analyse- und Speicher­systeme.
- **Historian / Datenbank**  
    Langfristige Archivierung von Phasordaten und Ereignisprotokollen (COMTRADE) für forensische Analysen und Netzmodell-Kalibrierung.
- **Visualisierungs- & Alarmierungs-Frontends**  
    Dashboard-Applikationen mit Spannungs-/Frequenz-Heatmaps, Phasoren-Traces und automatischen Grenzwert-Alarmen.
- **Analyse- / Steuerungs-Module**  
    State Estimation, Contingency Analysis, Wide-Area Protection und Remedial Action Schemes (WAMPAC), die auf Basis der Phasordaten automatisierte oder manuelle Eingriffe auslösen.

### 2. Hauptfunktionen

1. **Echtzeit-Monitoring**  
    - Verteilung von Phasor-Streams über IEEE C37.118.2 (IEC 61850-90-5) an einen oder mehrere PDCs.  
    - Anzeige von Drift, Phasor-Ungleichheiten und Frequenzabweichungen in Dashboards.

2. **State Estimation & Systemmodellierung**  
    - Ergänzung klassischer SCADA-Messwerte durch hochfrequente Phasordaten zur präziseren Modellierung des aktuellen Netz­zustands.

3. **Events-Erkennung**  
    - Automatisches Aufzeichnen und Kennzeichnen von Fault-Records (COMTRADE), Spannungs­sags und schnellen Frequenzauslenkungen (ROCOF).

4. **Weitbereichs-Schutz & Steuerung (WAMPAC)**  
    - Einsatz von Wide-Area Remedial Action Schemes, z. B. automatisches Lastabwerfen oder dynamisches Phasenschieben über HVDC-Leitungen.

5. **Post-Disturbance-Analyse**  
    - Nachbearbeitung von Störfällen anhand gespeicherter Phasor-Daten, um Schutz- und Steuerparameter zu optimieren.


### 3. Protokolle & Standards

- **IEEE C37.118.2 / IEC 61850-90-5** für Phasor-Data-Frames und Command-Frames
- **IEC 62351-5** für TLS-Sicherheit über IP-Transport
- **COMTRADE (IEC 60255-24)** für Störfall-Daten­archive
- **PTP (IEEE 1588)** für Sub-µs-genaue Zeit­synchronisation


> **Kurz:**  
> _Ein WAMS schafft weiträumige Transparenz im Verbundnetz, indem es synchronisierte Phasor-Messwerte zentralisiert, analysiert und für Monitoring, Schutz und Steuerung auf Netzebene bereitstellt._