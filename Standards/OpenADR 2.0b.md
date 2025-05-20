## Zweck & Anwendungsgebiet
- Offener Standard für **automatisierte Demand Response (DR)** zwischen Ener­gie­versorgern/Aggregatoren (VTN) und Endpunkten (VEN).
- Erlaubt zeit- und preis­gesteuerte Last- und Erzeugungsanpassungen.

## Architektur & Message-Flows
- **VTN (Virtual Top Node)** ↔ **VEN (Virtual End Node)** über SOAP/Web-Services.
- Kerndienste (OASIS Ei):
    1. **EiRegisterParty**: Registrierung und Vertrauensaufbau
    2. **EiEvent** (`oadrDistributeEvent`): DR-Event-Ankündigung        
    3. **EiReport** (`oadrCreatedEvent`, `oadrResponse`): Status- und Verbrauchs-Reporting
    4. **EiOpt**: Verfeinerung von DR-Signalen durch VEN        

## Datenmodelle & Datentypen
- **XML-Schemas** für Events, Reports, Registration:
    - Zeitfenster (Start/Stopp), Signaltyp (LOAD, CURTAILMENT, SCHEDULE)
    - Preis- und Leistungsparameter, Event-ID

## Security
- **[[TLS]] 1.2/1.3** mit [[X.509]]-Zertifikaten
- **WS-Security** (optional) für Message-Level Signaturen (XML-DSig) und Verschlüsselung
- Profile A (Basis), B (mit EiOpt & erweiterten Reports)

## Typische Use-Cases
- Registrierung von Laststeuergeräten (Smart-Thermostate, EVSE)
- Automatisches Absenken von Spitzenlasten bei Überlastwarnungen
- Lastverschiebung nach dynamischen Tarifen