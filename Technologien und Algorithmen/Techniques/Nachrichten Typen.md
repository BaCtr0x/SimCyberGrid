## InfoReport vs Data Frame
Ein **InfoReport** (TR-03109 / FNN) und ein **Data Frame** (IEEE C37.118) sind zwei völlig unterschiedliche Nachrichtentypen, die aus verschiedenen Normen stammen und für verschiedene Zwecke im Netz gebraucht werden.

|Merkmal|**InfoReport**|**Data Frame**|
|---|---|---|
|**Norm-Welt**|BSI TR-03109-1 / FNN-„Mikroprozesse“|IEEE C37.118 (Synchrophasor)|
|**Zweck**|Periodische Messwertlieferung des Smart-Meter-Gateways (z. B. Spannung, Strom, Energie) an VNB-Backend|Hochfrequente Phasor-Streaming-Daten (Vektor U/I, Frequenz, ROCOF) für Echtzeit-Stabilitäts­funktionen|
|**Typische Rate**|1 s (TAF 14) bis 15 min (TAF 9)|10 – 60 fps (≙ 16,7 ms – 100 ms)|
|**Inhalt**|Liste `measuredValue` mit Feldern `obis`, `value`, `unit`, `scaler`, `dlmsDataType`|Zeitstempel + Arrays `phasors[]`, `frequency`, `analog[]`, `digitalStatus`|
|**Serialisierung**|XML oder JSON nach FNN-XSD/JSON-Schema; HTTP + TLS|Binär oder IEEE C37.118-ASCII; meist UDP/IPv4, bei WAN: IEC 61850-90-5 (+ TLS)|
|**Signatur / Sicherheit**|CMS-Signatur + TLS-Kanal obligatorisch (TR-03109)|Optionale CMS-Signatur im IEC 61850-90-5-Container; Transport-TLS empfohlen|

### Warum tauchen beide in den Anforderungen auf?
- **InfoReport** nutzt dein Kommunikations-Simulator für alle SMGW-basierten Use-Cases (Netzzustands­überwachung, CLS-Steuerung).
- **Data Frame** kommt bei Grid-Stability-Szenarien ins Spiel, in denen Phasor-Messungen (PMU/µPMU) in Sub-Sekunden-Auflösung verarbeitet und in Echtzeit an WAMS-/SCADA-Algorithmen weitergeleitet werden.