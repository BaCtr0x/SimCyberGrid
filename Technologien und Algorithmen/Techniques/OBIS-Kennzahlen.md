OBIS-Kennzahlen, wurden einst auch EDIS-Kennzahlen genannt und werden bei der elektronischen Datenkommunikation in der Energiewirtschaft eingesetzt, um Messwerte wie Energiemenge (Zaehlerstand) oder Leistungswerte und auch abstrakte Daten in den Nachrichtentyp MSCONS und UILMD eindeutig zu identifizieren.

Die Kennzahlen sind dabei nach dem folgenden Muster augebaut$$A - B : C.D.E*F$$
Dabei stehen die Buchstaben fuer folgendes:
- $A:$ Medium (fuer Elektrizitaet (Strom) = 1; Thermische Energie (GAS)= 7)
- $B:$ Kanal (interne oder externe Kanaele, nur bei mehreren Kanaelen)
- $C-E:$ je nach Energie-Art unterschiedliche Bedeutung
- $F:$ wird im deutschen Energiemarkt NICHT verwendet

## Elektrische Energie
- $A = 1$
- $B:$ wie in der generellen Definition
- $C:$ Messgroesse (Wirk-, Bling-, Scheinleistung, Strom, Spannung, ...)
- $D:$ Messart (Maximum, aktueller Wert, Energie, ...)
- $E:$ Tarifstufe
- $F:$ Vorwertszaehlerstand (weiterhin nicht in Deutschland verwendet)

## Thermische Energie
- $A = 7$
- $B:$ wie oben
- $C:$ Messgroesse/-Qualifikation (Quelle, Richtung, Qualifikation der Messung, Datenprofil)
- $D:$ Zeitbezug; Messgroesse/-Qualifikation
- $E:$ Zeitbezug (Zaehlerstand, Differenz/Maximum/Mittelwer fuer Periode)

