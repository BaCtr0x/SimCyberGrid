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
- [ ] schauen wie SGCG und MEDIT an das komplexe allgemeine ding rangegangen sind 