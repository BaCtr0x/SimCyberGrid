### Notes for Meeting 05.03.2025
- [x] Milena fragen wegen meinen eingetragenen Zeiten
- [x] Wie wollen wir weiter machen? Ich kann so weiter machen, aber die Informationsdichte ist gering und fuer Leute wie uns, die nicht in dem Thema sind ist es schwierig zu sehen was wichtig ist und was nicht und wo man noch mehr Informationen herbekommen koennte, um gewisse Luecken zu schliessen
- Liste von Kolja durchgegangen und fuer uns wichtige Use Cases rausgesucht
- leider gibt es keine genau Beschreibung der Use cases, somit fuer leien wie mich schwer zu sehen was da alles genau hintersteckt
- Versucht noch was darueber raus zu finden, hat leider nicht geklappt
- Danach mich an EPRIM gesetzt und da weitere Use Cases rausgesucht

### Meeting 06.03.2025
- Montag einmal schreiben wie weit ich mit dem Clustering gekommen bin. Soll mir erstmal die anschauen, die aus dem Epri kommen. Wenn ich nicht soo richtig vorran komme, dann am Montag einmal bescheid sagen und etwas abgeben.

### Notes for Weekly 11.03.2025
- [x] Milena Zeiten Pausen Problem
	- einfach die Pausenzeit so obendrauf hauen und dann passt das am ende 
- [x] Sicherheitsvektoren aus Watson anschauen, wenn ich Zeit habe


### Notes Weekly 13.03.2025:
- Moritz und Sascha schreiben gerade Publikation ueber Metriken fuer False Data injection 
- Moritz hat Clustering mit Use Case in mehreren Clustern umgesetzt, ganz gute Idee
- Vielleicht kann man gut bei Customer Premis schauen was nur dazu gehoert kann man gut rausnehmen
	- Koennen wir schauen was davon einfach als BlackBox angenommen werden kann
- muessen auch schauen wie wir das umgesetzt haben, was alles von den Customer selbst kommt, wie man das einbauen kann, dass der User auch einfach nur Muell an Daten abgibt
- EMS selbst nicht simulieren, das wird zu viel und ist auch zu wenig reguliert, da gibt es zu viele unterschiedliche Protokolle, die alle irgendwie was eigenes machen 
- Hardware Zugriffe und Co sind eher Sicherheitsprobleme/Angriff und nicht ein Use-Case in dem Sinne
- Als Angriff betrachten, dass man sagt es laufen Anlagen zum falschen Zeitpunkt, ob das Marktmanipulation ist oder was anderes ist da egal 
- Mal schauen wie man den Workshop moeglichst gut darstellen kann. Macht erstmal Felix

### Notes Milena Weekly 18.03.2025
- [x] Wie granular sollen die Use Cases sein? Es gibt ein paar die man zusammenfasse koennte 

- kann mal ein Dokument erstellen mit den Sicherheitsangriffen die in MEDIT aufgelistet werden
- Am Donnerstag mal fragen welche Use Cases essentiell sind und wo man genauer mal in Angriffsvektoren reinschauen kann 
	- Status, Events und Befehle koennte schon einer der wichtigste sein 

### Notes Weekly 20.03.2025
- Gibt eine Paper von Sascha und Moritz als Kurzpaper, wo es um unseren Simulator geht und danach kommt dann das Paper von Moritz mit den False Data Injektion Metriken 
- Moritz fragt nach Essenskasse fuer Workshop und Felix auch
- Priorisierung dann auch auf Cluster und nicht auf den Use Cases
	- Wir bereiten einmal vor was hinter den Clustern steckt, mit ein zwei Use Cases als Beispiel, damit es nicht zu abstrakt wird
- Rahmenbedingungen auch angeben, also was haben wir an Personal, Hardware, welche Software verwenden wir und dann koennen die gut damit arbeiten und besser priorisieren 
- Die Anderen schauen schonmal was es fuer essentielle Use-Cases gibt und dann koennen wir schonmal ne angriffsanalyse fuer die machen 
- Naechste Woch dann konkrete Aufgabenverteilung fuer den Workshop machen
### Notes Milena Weekly 25.03.2025
 - Koennen fuer die Angriffe auch das SGAM model verwenden, da es noch die Layer gibt in denen auch das Information und Communication Layer liegt, da kann man dann gleich die Angriffe rein mappen und hat eine gute Uebersicht
	 - Wird zum Teil auch in dem SGCG Paper schon gemacht, muss ich mir aber nochmal genau anschauen wie weit sie da gehen und ob die layer genau beschrieben werden, damit man ein gutes mapping machen kann. Ist in den meisten faellen unwichtig, aber was dann in das Function Layer gehoert ist wichtig. Function scheint sich auf das business layer zu beziehen und koennte somit fuer uns unwichtig sein.
	- Standards in dem Sicherhietspaper sind schon gemappt auf Layer und Domain, genauer ansehen, welche fuer uns wichtig sein koennen und nachschauen ob die noch relevant sind 
	- denke wichtige layer sind: Information, Communication und Component layer
- KOmmunikation ist immer wichtig, kann ich mir genauer anschauen 
- Was sicherheit angeht uach nochmal in die BA die ich von Milena bekommen habe schauen
- Stride als Bedrohungsanalyse im Antrag angegeben 
- vielleicht scenairen beschreiben, in denen wir dann Sicherheitstests machen koennen und man hat einen besseren ueberblick, vielleicht zwei Scenarien an den Enden, also kleines Dorf und dann einmal groesser
- Donnestag mal Fragen welche grossen Gegensaetze gibt es, ist gross und klein richtig oder eher auf Spannungsebene
	- Auch in dem SGCG Dokument mal nachschauen und Sascha Fragen, ob die Scenarien definiert haben
	- Vielleicht auch in den Worksop nen Scenario aufbauen, dann hat man ein Kundenspecifisches welches relevant ist, vielleicht gleich am Anfang ein scenario definieren
- [x] einmal SGAM genau aufschrieben
- [x] schauen wie SGCG und MEDIT an das komplexe allgemeine ding rangegangen sind 
- [x] Ba von Milenas Studi nochmal anschauen

### Notes Weekly 28.03.2025
- Praesentation vom Projekt noch so auf 3 Folien aufbauschen
- Fragebogen macht Felix und vorbereiten des Raumes macht er auch 
	- Koennen danach auch gemeinsam in die Mensa gehen oder so und die meisten kommen wahrscheinlich so an, dass die schon gegessen haben. Ich sollte mir also lieber was mitbringen
- TRL (BSI) fuer die Sicherheit von Smart Meter Gateway, sind aber auch in NIS2 drin
- Sascha erstellt eine Liste mit allen Angriffen die er finden kann und laesst die dann von Merlin von Stromnetz Hamburg priorisieren. Damit haben wir dann auch schon eine gute Uebersicht. 
- Naechste Woche einmal Merlin mit in dem Meeting haben damit er einmal sagen kann ob wir auf dem richtigen Track sind.
- Nebenbei schon mal ein paar Punkte was wir so brauchen und wie das mit Hardware in dem Workshop anstossen (Felix fragt Merlin mal und sonst naechste Woche fragen)
- Was brauchen wir noch an Software? Ausm Stand brauchen wir wohl nicht wirklich was oder? Hat OWASP Kosten?
- Monopoly vielleicht mitbringen, damit wir geld haben fuer die Priorisierung

### Notes Milena Weekly 01.04.2025
- Freitag schonmal schaerfen was genau der SImulator koennen soll und dann schauen wir damit in dem Workshop weiter wie genau wie damit auch Sicherheitskram machen koennen
- [x] Kurze Zusammenfassung schreiben nach dem Workshop an Milena schreiben
- [x] Ich schau mir die alten Angriffe wie Stuxnet und co an, am besten schon einen fuer Freitag vorbereiten

### Notes Weekly 04.04.2025:
- Wie erwartet ist es fuer HNE irrelevant was hinter dem Zaehler passiert, es geht nur darum was bei denen ankommt und was es fuer auswirkungen haben kann. Das wir das im Hintergrund simulieren ist recht irrelevant
- Fokus bei uns ist mehr bei den Verteilnetzen und nicht primaer Microgrids, weil das andere interessanter ist und weitreichender ist. Vorallem weil die angriffe auf Microgrids zum Teil verhindert werden koennen indem dann einfach das Grid abgeschaltet wird.
- Angriffe koennen auch allgemein sein, da wir von HNE nichts genaues bekommen koennen und wenn wir die aktuelle Angriffe abbilden, dann reicht es, wenn wir sehen koennen ob das netz resilient gegen den Angriff ist oder nicht. 
	- Also interessant wie sich die Angriffe, die vielleicht urspruenglich von behinde the meter kommen auf front of the meter auswirken. Also nicht relevant wie wir da rein kommen und sondern was man dann machen kann. Koennte auch interessant sein, ob man sowas wie authentication escallation und andere unauthorized accesses umgesetzt werden koennen, wenn man von behind the meter kommt
	- Welche Angriffe lassen sich auf Front of the Meter ausfuehren, weil die Kommunikation nicht mehr so gerichtet und geschuetzt ist, wie es vorher war, sondern jetzt auch ueber wireless networks arbeitet


## Workshop 08.04.2025
- Einmal nachschauen wie jetzt die Rollen der Partner sind, damit die Rollenverteilung stimmt und auch jeder weiss ob er assozierter oder Beteiligter Partner ist, damit die Gelder am Ende auch laufen
- Die finale Version des Antrages ist nicht bei HNE/Merlin angekommen
- MIttelspannung scheint auch interessant zu sein, weil dort auch immer mehr Ausbau in der Ebene passiert und dort die Smart Messungen stattfinden. Muss ab 2026 eingebunden werden.
- Interessant was von Niederspannung auf die Mittelspannung fuer Auswirkungen haben koennte und was wir am Ende erzeugen koennen
- Zum Teil werden nicht kritische Informationen ueber Lora kommuniziert, muss ich mir mal ansehen, scheint aber kein sicherer Kanal zu sein
	- Lora ist sehr enegieeffizient, aber halt nicht besonders sicher
	- Kommunikation soll ueber GSM und LTE passieren, nichtmal 5G und auch nicht 450MHz:D
- Scope fuer das Projekt als HAW und TH abstecken, damit wir nicht ueber unsere Masse gehen und damit das Projekt nicht aus dem Ruder laeuft, vor allem auch im Bezug auf Hersteller und Behinde-the-Meter. 
	- Nach VDE ist Behinde-the-Meter sehr interessant.
	- Behinde-the-Meter ist eher der Forschungsbereich, aber die Auswirkungen sind in Front-of-the-Meter interessant, weil dort eben HNE liegt und fuer die dort die Auswirkungen ankommen
	- Aktuell ist die Auswirkung die Homeanlagen haben noch nicht soo relevant, weil es noch das Stromnetz nicht lahmlegen kann, aber wenn das so weiter geht wie es aktuell passiert, dann wird das bald der Fall sein, also ist das auf jeden Fall sehr relevant wie man auch auf der Ebene dann in die Front-of-the-Meter Auswirkungen ballern kann.
- Wie von uns gedacht mit den Angriffen betrachten wir die Auswirkungen von Angriffen und Abstrahieren von wo was kommt, also sowas wie zerstoerte Objekte sind am ende nicht sonderlich anders als wenn das Objekt einfach nicht mehr erreichbar ist und auch nichts mehr macht.
	- Dabei kann man dann gut in unterschiedlichen Ebenen abstrahieren, also Wo kommen die Werte her und wie kommen die irgendwo rein
- Gewuenscht von Dawood, dass die Nutzung von dem Simulator einfach ist, damit das am Ende ueberhaupt jemand nutzt, aber am Ende ist es ja mehr eine Sache von Monesi, ausser die Angriffe, dass dort ein einfaches Interface oder so ist, damit das auch genutzt wird und nicht verstaubt 
- Idee von Merlin, dass man versucht den Simulator von vornerein so aufbaut, dass man den in der Lehre verwenden kann, also das der fuer die TH und die HAW verwendbar ist, weil sowas wie HNE das Ding am Ende nicht nutzen wird, weil die das nur nutzen um zu sehen ob es gebraucht wird und dann wird es kommerziell eingekauft. 


## Weekly 10.04.2025:
- Schauen welche Use-Cases wir jetzt alle rausschmeissen koennen und wie wir die mappen koennen in der Excel. Dann eine Threshold bestimmen, damit wir damit was rausschmeissen koennen. 
- 25.04. am FTZ ist letzter Tag von Moritz. Kann vielleicht vorbeischauen 
- HiSolutions schaut Sascha nach was man da machen kann und ob Volker mal einen ordentlichen Kontakt mitbringt
- Poster fuer SimCyberGrid machen, mir mal ueberlegen, was ich da von der Sicherheitsseite aus machen kann 
- Wissenschaftliches Review, bzw mal ein Dokument mit den Use Cases und Co zum Vorzeigen bis 25.05. basteln


## Weekly Milena 15.04.2025:
- [x] Wie wollen wir das mit Threat Modeling machen? Wir koennen zum einen eine Threatanalyse machen mit sowas wie STRIDE oder Attacktrees, aber das deckt ja nur einen Teil ab, der am Ende auch nicht soo relevant ist. Wollen wir dabei dann lieber was anderes nehmen, damit wir Angriffe auf das Netz betrachten, wie eher auf die Netzstabilitaet bezogen sind?
- [x] Soll ich dann schon mal versuchen eine grobe Version eines Data Flow Diagrams (DFD) zu erstellen?
- [x] Wollen wir eigentlich in dem Simulator auch Mitigation techniques identifizieren und umsetzen oder ist es am ende mehr ein "so ist der aktuelle Stand und wenn man angriff X drauf faehrt, dann passiert Y?". So wirkte es zumindest von HNE aus, dass die daran interessiert sind, was man alles machen kann und vor allem auch was man als Angreifer von Behinde the Meter machen kann um Auswirkungen auf Front of the Meter zu haben.
- DFD erstellen und anhand von vielleicht STUXNET die unterschiedlichen Threat analysis tools ausprobieren. Vielleicht ist noch was besser als risk matrix with attack trees
- Weitere Angriffe raussuchen
- Nachfragen ob GSM wirklich richtig war, weil 2G scheint mir sehr unsicher


## Weekly 17.04.2025:
- [x] Meinte Merlin wirklich GSM und nicht UTMS, weil GSM ist 2G und da kam vor 2 Jahren erst nen Paper raus, das gezeigt hat, das GEA-1 und GEA-2 unsicher sind, also die Verschluesselungen von 2G und nicht mehr aktuell sind.
- Einmal schauen was wir haben und was wir fuer die Use Cases brauchen damit man die in dem Simulator umsetzten kann. Das muessen wir einmal klaeren, damit wir damit dann weiter machen koennen, weil der Uebergang zwischen was in Hardware da ist und was in Software gebraucht wird, bzw. wie man das umsetzen kann.
	- Es gibt aber Vorgaben vom BSI und der Netzagentur ueber die die Kommunikation funktionieren soll. 
	- Wir machen also eher eine Vorstellung von der Umsetzung und muessen dann schauen was da wirklich passieren soll und damit wir uns nicht irgendwas komisches ausdenken 
	- Einmal suchen welche Vorgaben gibt es da schon sei es in Dokumenten von beispielsweise dem BSI und anderen Agenturen und dann schauen was wir noch selber aufbauen muessen
	- Bis naechsten Woche einmal schauen ob man von Use Case oder von Paragraph 14 a kommen kann und schauen was man da so zusammenbasteln kann, kommt dann von Moritz und Felix
	- Darauf basierend kann ich dann auch nen Dataflow Diagram machen und dann weiter mit den Angriffen arbeiten 
	- Kann mir auch weiter die Angriffe anschauen, dann koennen wir die nutzen wenn Felixes Ansatz funktioniert. Und sonst schon mal die Technischen Vorgaben fuer die Kommunikation anschauen. 

## Weekly 24.04.2025
- Moritz hat schon mal einen Ansatz erstellt und kann damit dann zeigen was er sich ueberlegt hat. 
	- Cluster als Kategorie, dazu dann den Use-Case
	- und dann stellen wir die drei Anforderungspositionen des Simulators vor, also:
		- Kommunikationssimulation
		- Stromnetzsimulation
		- Co-Simulation
		- Testfall (kam von Milena)
	- Die koennen wir dann fuer alle Use-Cases machen
- Felix macht es auf graphischer Natur, ist aber schon eher Threatanalyse. 
	- Hat ein Beispiel vom Frauenhofer
	- Schauen was man bei der Abbildung dann pro Komponente an Protokolle hat
	- Auch schauen was man dann fuer Angriffe auf die Teile fahren kann.
	- Auch interessant, PV is ENWG und dadrunter ist dann alles Paragraph 14
	- Das Bild ist alles behinde of the meter und dann front of the meter ist alles vor dem CLS Kanal
- Bauen uns ein Beispiel in der Tabelle von Moritz, dann haben wir schon mal einen Ansatz mit dem man arbeiten kann und dann auch schauen kann ob man Felixes Graphic gleich nutzen kann.
	- Dabei auch genau schauen welches Format die Daten haben und wie diese Kommuniziert werden, also als JSON oder so und welche Encryption wird darauf gefahren und was muss der Simulator an der Stelle koennen (also ist das einfach nen Smart Meter Gateway das einem einen Wert gibt? Oder haben wir einfach Lastprofildaten oder aehnliches, muessen wir eh zum Teil ueber Profile machen, da wir nicht alle Haushalte in einem Niederspannungsnetzscenario simulieren koennen.)
	- Eine BeispielJSON ist in Moritzes MA oder aehnliches 
	- Extra fuer die Co-Simulation brauchen wir nen JSON Parser, der die erstellt und auch wieder einlesen kann
	- ==Gibt es eine Pruefung ob das Format richtig ist oder gibt es die gar nicht, dann kann einem ja uebergeben was jemand will und was dann passiert?==
	- Brauchen positiven und negativen Testfall
	- Koennen das noch bei Felixes graphischer Version einbinden oder so eine grobe Threatanalyse machen mit Assets und Co
- Ueberlegen was man als JIRA nutzen koennen, gibt es ne kostenlose Version? Vielleicht nen Gitlab oder so? Nen Github mit 2FA wuerde ja auch gehen
- Einzel als Use-Case stimmt das Format und sind die Werte in einem passenden Rahmen und schauen ob wir die in einem bereits ausgewaehlten Use-Case schon haben
- Mal schauen was unter Tarifliche Leistungen in der TR zu finden ist, da ist Kommunikation mit Kommunikationsfrequenz und Co. 
	- Schauen welche wir davon brauchen und welche davon schon mal unter welche unter die Use-Cases fallen
	- Minuetlich (TAC 14) und alle 15 Min (TAC 7) schein sinnvoll zu sein
- Jeder such sich nen Cluster raus und Use Cases und macht das schon mal in der Tabelle eintragen 

## Weakly Milena 24.05.2025
- schon gleich mal in der Anforderungsanalyse auch gleich mal Threats die einem Auffallen mit-notiert
- vielleicht ne Threatanalyse mit STRIDE und Attack Tree
- [x] Schon mal das Beispiel von Heute mit Assets und Threats aufschrieben, damit man ein vollstaendiges Beispiel haben
- [x] Bei Moritz das Beispiel mit der JSON suchen und schauen was da alles zu erwaehnt wird. 
- [x] David Engelhard und Daniel Kratzge mal schauen ob man das Gitlab fuer Forschungsprojekte nutzen kann und was Github so kann an Educational kram machen kann 
	- vielleicht gibt es ja sogar nen Portformat von Excel auf Github/Gitlab oder anderes
	- Sebastian auch mal fragen was man so als alternative nutzen kann


## Weekly Milena 29.04.2025
- Das Beispiel der Anforderungen sollten genauer sein
- [x] aufschrieben was sind die Schutzziele, sodass man fuer die Use-Case Anforderugen dann auch etwas allgemeineres hat, um sowas wie eine Priorisierung hat, also sowas wie Hauptproblem ist Datenmanipulation [[Schutzziele]]
- [ ] Gibts im praktischen bereich raussuchen was man als beispiele hat fuer angriffe und vielleicht finde ich das jemanden der das mal als Beispiel an irgendwas durchgeht
	- raussuchen wie gehen die mit der komplexitaet um und wie kann man damit dann arbeiten um auch fuer uns weitere 
	- Auch mal schauen ob es nen Medit talk gibt [gibts nicht]
	- Kann auch aus nem anderen Projekt oder Bereich kommen, mal weiter im Verteilensystembereich schauen 
	- Einfach schauen ob ich was finde, was mir sagt wie man die Threats etwas reduzieren oder verallgemeinern kann ohne in Bereichen zu ungenau zu werden

## Weekly Milena 06.05.2025
### Notes for the Meeting
- Habe nicht alles von Donnerstag geschafft, weil ich etwas fuer die Doktorarbeit gemacht habe und dann von den 32 Dokumenten vom BSI zu SMGW abgelenkt wurde, da koennte einiges drinstehen was wir brauchen, wie Anforderungen an unseren Simulator und Testfaelle, aber das dauert noch ein bisschen bis ich das auf unseren Kram mappen kann. Denke aber erstmal das da schon einiges drinsteht, was wir brauchen werden.
- Anforderungen in TR-03109-1 beschreibt die Anforderungen an das SMGW und die notwendigen Sicherheitsprotokolle. Es soll laut ChatGPT auch alles genau spezifiziert sein, also auch die Formate der jeweiligen Werte in den Dateien, aber das habe ich noch nicht so gut gefunden, ist aber auch sehr viel zum durchschauen
	- Fuer alle zu Protokollierenden Anforderungen und Parameter, die in den Anforderungen aufgelistet werden, gibt es ab Seite $311$ auch eine Tabelle mit groben Fehlermeldungen und den zugehoerigen Datentypen fuer die beteiligten Parameter.
- Testfaelle sind in einem Dokument festgehalten das unter TR-03109-1 Testspezifikation zur Technischen Richtlinie TR-03109-1
	- Scheint relevant fuer uns zu sein, weil dort auch definiert wird, was getan werden soll, wenn beispielsweise das XML Format nicht stimmt und welche Fehlermeldung ausgegeben wird. Vielleicht kann man also fuer all die Faelle einfach auf das Dokument verweisen
- Ich habe einmal Schutzziele aufgeschrieben, kann die nachher mal als Excel oder so aufschreiben und dann in Teams werfen. Leider kann man in Teams nicht Markdown bearbeiten, sonst heatte ich das einfach da hochgeladen
- In BSI TR-03109-1 Anlage I: CMS-Datenformat fuer die Inhaltsdatenverschluesselung und -signatur werden wie der Name erahnen laesst die Datenformate fuer die Inhaltsdatenverschluesselung und -signatur spezifiziert, dabei gehen sie auch soweit und stellen Datentypen da, wie bit string
- Ich habe David Engelhardt angeschrieben wegen GitLab, aber noch keine Antwort bekommen. Sebastian wusste leider auch nicht ob das fuer externe nutzbar ist. 
- Bei den Anforderungen muss das so formuliert werden, dass es sich dicht an dem realen Bild orientiert oder waere sowas wie:
  Jeder Messwert, den der Netz-Simulator generiert, wird vom Kommunikations-Simulator in einen `InfoReport`-Container serialisiert.

### Notes from the Meeting
- thread analyse Beispiele raussuchen, welche es auf Verteiltensystemen gibt, damit man mal ein Beispiel hat und sich daran orientiren kann
- am ende eher grob in den Anforderungen blieben und nicht soo detailiert bleiben und dann lieber agieler aufbauen 
- [ ] Fuer Donnersag prio dass ich ne uebersicht uber die BSI Dokumente machen und dann darueber sprechen was wir da raus nehmen koennen


## Weekly 08.05.2025
- Grundlegend wuerde ich sagen, dass es sinnvoll ist, wenn ich eher mich auf die Kommunikation beschreanke, da kann ich mich noch ganz gut bewegen, aber sobald das an Stormnetzspezifische Punkte kommt und vor allem Hardware bin ich eher raus
- Cluster die ich uebernehmen kann sind:
	- **System and Security Management** (Fraglich wie weit man da Anforderungen aufbauen kann oder ob das am Ende eher eine Sache ist von Security muss halt stimmen)
	- **Monitoring the Grid flows**
	- **Collect events and status information**: Ist wahrscheinlich sinnvoll das mit zu nehmen, weil das dich zu Monitoring the Grid flows gehoert oder?
- Naechste Woche ist Tag der Energie da muss ich in Bergedorf sein
- Erste Zeile Assets sind alle die wir brauchen fuer das Smart-Grid, also reicht das schon
- Einmal das Grid last Diagramm darstellen und dann abklaeren
- [ ] Felix einmal Fragen ob er mir die Folien von Kolja schicken kann, die er in dem Meeting hatte 
- Wenn system wie SCADA unbekannt ist, weil es da unterschiedliche Optionen gibt, dann lieber ein System aufschreiben, welches Anforderung XY kann und nicht festlegen mit SCADA betiteln $\rightarrow$ also was wir wissen koennen wir aufschreiben, der rest bleibt dann als etwas undefiniertes System, was etwas koennen muss
- [x] 16:30-17:00 mit Felix nochmal zusammensetzen und dann einmal durch die Use-Cases mit den Anforderungen machen, kann auch grob sein
- 

## Notes Meeting Sofie 09.05.2025
- Arbeiten primaer auf Niederspannungsebene und machen da dann das UX. 
- Sofie ist fuer das UX verantwortlich und Alex hilft dabei und macht noch was anderes (wieder vergessen)
- Wollen uns alle 2 Monate mal treffen und besprechen was sich bei wem getan hat
- Habe vorgeschlagen, dass wir uns mit bei denen orientieren, ist sinnvoller, da die schon Anforderungen haben und wissen was sie abbilden wollen. Also wenn wir das Backend von denen sind, dann muessen wir schauen, dass wir das abbilden, was die brauchen.
	- Dabei auch mal Sascha fragen, ob wir die Anforderungen von Monesi bekommen koennen, dann kann man da mal schauen was die noch so haben und gucken ob wir das beachten muessen oder ob das bei uns schon mit drin ist.
- habe deren UX design fuer die Niederspannungsuebersicht gesehen, sieht gut aus, aber viele Details fehlen noch, also noch nicht soo informativ fuer uns, aber das wird noch werden, denke das wird interessant werden, damit wir auch wissen wie wir Fehlermeldungen handhaben sollten

## Notes Meeting Felix 09.05.2025
- [x] Ist ein LoadShedding immer das gleiche, ob fuer spannung oder frequenz?
- [x] Sind Operate DER, Protecting Grid Assets und Blackout management noch relevant?
- Sollte ja aber gut gehen, wenn wir so wie heute arbeiten, dann kann ich meinen Teil bis naechste Woche fertig haben
- 

## Notes Milena 13.05.2025
- 

## Notes Weekly 15.05.2025
- [x] Sascha fragen ob wir die Anforderungen von Monesi bekommen koennen
- [ ] 

## Notes Milena 20.05.2025
- [ ] David GitLab fragen und auch mal schauen ob ich den so auf dem Flur sehe, koennte schneller gehen
- [x] Praktische Beispiele fuer Angriffe und Analysen raussuchen
- [x] Dataflow Diagram und Tabelle aufbauen


## Notes Milena 03.06.2025
- [x] Was wurde Besprochen?
	- war nicht da und muessen schauen wie es weiter geht
- [x] Was sind die weiteren Plaene?
	- siehe TODOs
- Habe eine Case Study gefunden, die STRIDE verwendet und die Stellen eine Threat Analyse auf und validieren diese dann mit beispielsweise Stuxnet, um zu sehen ob die passenden Threats abgedeckt sind

### $\rightarrow$ TODOs
- [ ] Sicherheitsanalyse anfangen und dann schauen aehnlich zu STRIDE aber schon eher Assets-based
- [x] Trike analyse mal ansehen, koennte gut sein, aber wissen wir ueberhaupt was wie riskant ist
- [ ] Schutzziele und Assets aufzubauen und dann schauen ob STRIDE oder Attack Trees sinnvoll sind
- [ ] Auch Use-Case maessig durch die Assets und Co gehen
- [x] Email an Haustechnik schreiben und dann sagen, dass ich zugriff auf den Schluessel fuer Haus 18 bekomme :D


## Notes Milena 10.06.2025
- In dem Paper machen die STRIDE sehr genau und nehmen jede Operation die jedes Teil machen kann als ein Variable und dann geben sie fuer alle Angriffsbereiche wie Spoofing an welche Operationen, bzw. welcher Datanfluss wo reinfaellt. Brauchen wir das so genau oder reicht das groeber, also nicht mit read/write, Login und Co specifisch, sondern mehr component specifisch?
- [x] Hat Milena ueber Risks angesprochen, noch nicht weil nur Sascha da war
	- wenn wir die wissen, dann koennte Trike gut funktionieren, weil es eben auf DFD aufbaut und mit acceptable risks arbeitet, was wir in dem Stromnetz bestimmt haben werden, wie kleine Fluktuationen oder so. 
	- STRIDE ist aber gut um eine Basis fuer die Entwicklung zu haben, damit wir direkt wissen worauf wir achten muessen.
- Einmal Threat analyse anhand von einem Use Case machen 
	- gerne auch mit einer Ai machen und mal schauen was die unterschiedes sind, die man selber rausbekommt und was die bekommen
	- mit notizen machen, damit man den ganzen Process am ende als Paper aufbereiten kann 
- Donnerstag sehen was ide anderen so haben und den Fokus auf Test und Anforderungen setzen und dann schauen wie weit wer was machen soll 
- testfaelle sind wichtig, sonst wird angriffe fahren auch schwierig 
- Mal schauen wenn ich an den Punkt kommen an dem Routine kommt, ob es sinnvoll ist einen Studi einzustellen, aber das kann ich dann einfach bescheid sagen.
	- Vielleicht gibt es auch Projekte die sich anbieten oder Abschlussarbeiten die man dafuer nutzen kann 
### $\rightarrow$ TODOs
- [x] mal schauen ob ich das hinbekomme eine analyse fuer Trike und STRIDE fuer Donnerstag hinbekommen, anhand eines Beispieles, wie Use-Case


## Note Milena 17.06.2025
- [x] Soll ich sowas wie Protocol Downgrad, DoS oder Fingerprinting  als Threat in jede Kommunikation einfuegen oder machen wir ein paar uebergeordnete Threats die auf alle Kommunikationswege zutreffen?
- Darueber schon unsichere verwendete Protokolle gefunden naehmlich Modbus, DNP3 und IEC61850


## Weekly 19.06.2025
- Sascha hat die Tabelle mit den Anforderungen ueberarbeitet, sodass wir jetzt noch 63 Stueck haben und wenn er aus dem Urlaub kommt, naechste Woche weg, macht er mit den Testfaellen weiter
- Felix neue State Estimation vorgestellt 
	- messungen sind minuetlich und rollierende 10 Minuten Messwerte, sonst war 15 min eher normal
	- wollen auch mit einem der Leute die in dem Team aus dem Paper sitzen sprechen, wegen der Hill und der State Estimation, kommt noch in der Zukunft
	- SimBench und Realnetze verwendet
	- sinnvoll erstmal 15% ausstattung von Smartmetern annehmen, ist realistischer
	- wenn es mehr werden, koennte das noch kommen, aber ist noch unwahrscheinlich, koennen wir uns aber gut anhand des Papers ansehen
	- 
- Wollen auch SimBench Netze nehmen, sind deutsche Beispielnetze und gut zur simulation, um etwas unabhaengig von Stromnetzhamburg und der Zeit bis wir hardware haben zu sein
- 