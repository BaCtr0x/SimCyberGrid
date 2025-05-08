
## Overview of Smart-Meter-Gateway and its Environment
![[Smart-Meter-Gateway and its Environment.png]]

## Anschlussnutzer
Akteur am SMGW, der elektrische Energie, thermische Energie, Gas oder Wasser bezieht oder erzeugt und zur Nutzung des Netzanschlusses berechtigt ist. Der Begriff Anschlussnutzer umfasst auch die Bezeichnungen Letztverbraucher, Endkunde und Anlagenbetreiber die in [EEG], [EnWG], [MsbG] genannt werden.

## Smart-Meter-Gateway-Administrator
der Smart-Meter-Gateway-Administrator (GWA) ist für das SMGW die vertrauenswürdige Instanz und übernimmt dessen Konfiguration, Überwachung und Steuerung. Er erstellt und administriert die in das SMGW eingespielten Profile zur sicheren Anbindung von Kommunikationspartnern, zur Messwertverarbeitung (Erfassung, Speicherung, Verarbeitung und Versand), zur Verwaltung SMGW-interner Prozesse und führt bei Bedarf die Aktualisierung der SMGW-Firmware durch. Der GWA hat keine Einsicht in die Messwerte.

## Berechtigte Externe Marktteilnehmer (External Market Participant)
Externe Marktteilnehmer (EMT) sind aus Sicht des SMGW alle Teilnehmer im Weitverkehrsnetz mit Ausnahme des GWA, mit denen das SMGW eine Kommuynikation zum Austausch von Daten aufnehmen kann. Hierunter fallen z.B. der Verteilnetzbetreiber (VNB), der Messtellenbetreiber (MSB), der Energielierferant (LF) und sonstige autorisierte Dienstleister.

## Messeinrichtungen
Messeinrichtungen (eng. Meter, MTR) im Local Metrological Network (LMN) dienen der Erfassung von Verbrauch und Erzeugung von Stoff- oder Energiemengen, Erhobene Messwerte werden von der Messeinrichtung an das SMGW übermittelt.

## Steuerbare lokale Systeme (Controllable Local Systems)
Controllable Local Systems (CLS) sind Systeme mit IT-Komponenten an der HAN-Schnittstelle des SMGW, die nicht zum Intelligenten Messsystem gehören, aber das SMGW für bestimmte Kommunikationszwecke verwenden. CLS können von lokalen Erzeugungsanlagen über steuerbare Lasten wie Wärmepumpen, Ladegeräte für Elektrofahrzeuge oder Batteriespeicher bis hin zu Anwendungen in der Hausautomation reichen. Darüber hinaus werden Geräte für Mehrwertdienste unter dem Begriff CLS zusammengefasst. Ein CLS nutzt die HAN-Anwendungsprogrammierschnittstelle (API) für die Rolle CLS.

## Servicetechiker
Der Servicetechniker (SRV) des GWA kann am Einsatzort des SMGW im Wirkbetrieb eine lokale Diagnoseschnittstelle am SMGW nutzen, um lesenden Zugriff auf das System-Logbuch und weitere Diagnosedaten zu erhalten sowie das Gerät in engen Grenzen zu parametrieren. SRV kann sowohl die Person als auch das von der Person verwendete Komponente (z.B.Diagnosegerät) bezeichnen. Die Komponente des Service-Technikers nutzt die HAN-Anwendungsprogrammierschnittstelle (API) für die Rolle SRV.