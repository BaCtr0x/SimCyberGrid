**MMS (Manufacturing Message Specification)** ist das standardisierte **Client-Server-Protokoll** in [[IEC 61850]] für den Austausch von Steuer- und Messdaten in Umspannwerken. Es basiert auf dem ISO-9506-Standard und implementiert das in IEC 61850-7-2 beschriebene **Abstract Communication Service Interface (ACSI)**.

---

## 1. Protokoll-Stack & Transport
1. **Anwendungsschicht (MMS, ACSI)**  
    - Definiert abstrakte Services wie **Get**, **Set**, **Operate**, **DefineReport**, **Read**, **Write**, **GetDirectory**.

2. **Sitzungsschicht (ACSE)**  
    - Aufbau und Abbau von logischen Verbindungen („Association“) zwischen Client und Server.
 
3. **Darstellungsschicht (Presentation)**  
    - Kodierung der Datentypen in **ASN.1 BER** (Basic Encoding Rules).
  
4. **Transportschicht (ISO/IEC 8073 bzw. RFC 1006 über [[TCP]])**  
    - Kapselt OSI-TP0/TP4 über TCP/IP, um auf Standard-Ethernet-Netzen zu laufen.

5. **Sicherung & Integrität**  
    - In practice oft per **[[TLS]]** ([[IEC 62351]]-3) oder IPsec auf dem TCP-Transport geschützt.    


## 2. Verbindungsaufbau
1. **Association Request**  
    - Der Client sendet eine ACSE-“Connect”-Nachricht an den Server, inklusive gewünschter ACSI-Parameter.
   
2. **Association Response**  
    - Der Server akzeptiert (oder lehnt) die Verbindung, liefert Sicherheitsattribute (z. B. Zertifikatsinfo) zurück.

3. **Data Transfer**  
    - Nach erfolgreicher Association nutzen beide Seiten die ACSI-Services auf der offenen Verbindung.

## 3. Kern-Services (ACSI-Operationen)

| Service                          | Zweck                                                              |
| -------------------------------- | ------------------------------------------------------------------ |
| **Get**                          | Abfragen aktueller Werte (einzelner Data Attributes)               |
| **Set**                          | Ändern von Datenfeldern (z. B. Setpoint-Vorgaben)                  |
| **Operate**                      | Zwei-Stufen-Befehlsabwicklung (Select → Operate) für Schaltbefehle |
| **DefineReport** / **GetReport** | Einrichtung von periodischen oder event-basierten Reports          |
| **GetDirectory**                 | Auflisten von verfügbaren Objekten (Verzeichnis)                   |
| **Read/Write**                   | Bulk-Lesen und -Schreiben von Datenobjekten                        |

Jeder Service folgt dem Muster:
1. **Request** vom Client
2. **Response** vom Server (inkl. Daten oder Fehlercode)

## 4. Reports & Events
- **Report-Kontrolle**
    1. Client sendet **DefineReport** (Was? Wo? Wie oft? unter welchen Bedingungen?).
    2. Client sendet **CreateReport** (Aktivieren).
    3. Server sendet periodisch oder bei Event-Triggern **GetReport-Indications** mit den angeforderten Daten.

- **Event-Mechanismus**  
    - eports können bedingt durch Datenänderungen (z. B. Überschreiten einer Schwelle) automatisch ausgelöst werden.    

---

## 5. Typische Ablaufsequenz (Beispiel Schaltbefehl)

1. **Select**(CSWI1.Pos.stVal, ctlVal=1)
2. **Operate**(CSWI1.Pos.stVal, ctlVal=1)
3. Server bestätigt beide Schritte einzeln mit **SelectResponse** und **OperateResponse**
4. Nach Ausführung meldet das IED den neuen Status via Report oder unaufgeforderten GetReport.

## 6. Besonderheiten
- **Mandatorisch vs. Optional**: Viele LN-Elemente sind als mandatory oder optional gekennzeichnet; der Client muss mit optional fehlenden Feldern umgehen.
- **Performance**: MMS-Antworten liegen typischerweise im Bereich von wenigen Millisekunden, je nach Netzwerk- und IED-Leistung.
- **Fehlerbehandlung**: ACSI definiert standardisierte Fehlercodes (z. B. objectUninitialized, instanceUnavailable), die im Response-PDU zurückgegeben werden.


> **Kurz zusammengefasst:**  
> MMS ist der **OS-unabhängige**, **service-orientierte** Nachrichtenaustausch von IEC 61850, der über ACSE-Verbindungen auf [[TCP]]/IP (RFC 1006) läuft, Datentypen in ASN.1 kodiert und hochverfügbare Steuer- und Messanwendungen in Umspannwerken ermöglicht.