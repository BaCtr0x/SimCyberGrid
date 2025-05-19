**DNP3** steht für **Distributed Network Protocol, Version 3** und ist ein offenes, weit verbreitetes **SCADA-/Telemetrie-Protokoll** in der Energiewirtschaft, Wasser-/Abwasser-Branche und anderen kritischen Infrastrukturen.
### 1. Zweck & Einsatzgebiete

- **Primär** für die Kommunikation zwischen Leitsystem ([[SCADA - Supervisory Control and Data Acquisition|SCADA]]/DMS) und Feldgeräten (RTUs, PLCs).
- Weit verbreitet in Nordamerika, zunehmend auch in Europa, wenn IEC 60870-5-104 (IEC 104) nicht eingesetzt wird oder Interoperabilität mit nordamerikanischen Systemen gefragt ist.

### 2. Architektur & Schichten
- **Physical Link**: serielle Leitungen (RS-232/485) oder TCP/IP (DNP3/IP).
- **Link Layer (DNP3 LLC)**: Rahmenbildung, Adressierung (Master/Outstation), Fehlererkennung (FCS), Wiederholmechanismen.
- **Transport Layer**: segmentiert große Datensätze, stellt Reihenfolge und Bestätigung sicher.
- **Application Layer**:
    - Objektorientierte Struktur: _Data Objects_ (Binary Inputs, Analog Inputs, Counters, Control Relay Outputs …)
    - Funktionen: Lese-/Schreib-Requests, Spontan-Updates (Unsolicited Responses), Zeit-Synchronisation, Integrity Polls, Event-Polls.

### 3. Datenmodelle
- **Data Attributes**:
    - **Binary Input (1 bit)** – Zustand digitaler Sensores
    - **Analog Input (32 bit)** – Messwerte (Spannung, Strom, Temperatur)
    - **Counter (32/16 bit)** – Zählerstände, Energie
    - **Control Outputs** – Steuerbefehle (Operate / Select-Before-Operate)

- **Unsolicited Responses**  
    Outstations senden selbstständig Ereignis-Updates (Statusänderungen), ohne erst von Master abgefragt zu werden.
   
### 4. Zeitsynchronisation & Events
- **Time Sync**: Master kann eine zeitgerechte Synchronisation per “Time and Date” Command an Outstations senden.
- **Event Polling**: Outstation hält intern Änderungs-Events vor, bis Master sie mittels eines “Integrity Poll” abruft.

### 5. Sicherheit (DNP3 Secure Authentication)
- **DNP3-SA** (Secure Authentication v5): ergänzt das Basis-Protokoll um
    - **HMAC-basierte Signaturen** auf Nachrichtenblöcke
    - **Replay-Schutz**, **Sequence-Numbers**, **Key-Management**
    - Optional [[TLS]]/[[TCP]]-Encapsulation über DNP3/IP

### 6. Warum DNP3?
- **Robustheit** für langsame oder gestörte Leitungen (eingebaute Wiederholung, Poll/Unsolicited-Mechanismen)
- **Ereignisorientiert** (Reduzierung von Poll-Traffic, schneller Unsolicited-Versand)
- **Leistungsfähig** für große Netze mit vielen Feld­geräten
- **Offener Standard** (entwickelt von DNP Users Group), breite Herstellerunterstützung

> **Kurz:**  
> _DNP3 ist das Industrie-SCADA-Protokoll für zuverlässige, objektorientierte Telemetrie und Steuerung zwischen Leit- und Feldsystemen, erweitert um Secure Authentication für hohe Cyber-Security._