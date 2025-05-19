**ECDSA (Elliptic Curve Digital Signature Algorithm)** ist ein Verfahren, mit dem man mittels elliptischer Kurven **digitale Signaturen** erzeugt und prüft. Es nutzt dieselben Kurven wie [[ECDH]], ergänzt aber einen **Hashing- und Zufalls-Schritt**, um Nachrichten fälschungssicher zu signieren.

## 1. Schlüsselerstellung
1. **Kurve und Generator** wählen  
    - Öffentliche Parameter: Kurve „secp256r1“ (z. B.), ein Generatorpunkt $G$ mit Ordnung n.

2. **Privater Schlüssel**  
    - Zufällige Zahl $d \in [1, n–1]$.

3. **Öffentlicher Schlüssel**  
    - Punktmultiplikation: $Q = d \cdot G$ (ein Punkt auf der Kurve).    

## 2. Signaturerzeugung (Sign)
Gegeben: Nachricht **M** und Hashfunktion **H** (z. B. [[SHA]]-256).
1. **Hashen**  
    - $e = H(M) \mod n$ gekürzt.

2. **Zufallszahl**  
    - Wähle kryptographisch sicheren Nonce $k \in [1, n–1]$. 

3. **Punktmultiplikation**  
    - $P = k \cdot G = (x_1, y_1)$, berechne $r = x_1 \mod n$.  
    - Falls $r = 0$, gehe zu 2.
   
4. **Berechne s**$$s=k^{−1}\cdot (e+d\cdot r)\mod n$$
    - Falls $s = 0$, gehe zu 2.

5. **Signatur-Paar**  
    - $(r, s)$ ist die Signatur.

**Merkmale:**
- **Einmaligkeit von $k$**: $k$ darf nie wiederverwendet werden, sonst kann $d$ aus $(r, s, k)$ berechnet werden.
- **$r$ und $s$** sind jeweils $1\dots n–1$; wird typischerweise als $64$ Byte (bei secp256r1) abgespeichert.
   

## 3. Signaturprüfung (Verify)
Gegeben: Nachricht $M$, Signatur $(r, s)$ und öffentlicher Schlüssel $Q$.
1. **Gültigkeitsprüfung**  
    - Prüfe $1 \leq r, s \leq n–1$. Andernfalls Signatur ungültig.

2. **Hashen**  
    - $e = H(M) \mod n$ gekürzt.

3. **Inverse von $s$**  
    -  $w = s^{-1} \mod n$

4. **Koeffizienten**    $$u_1 = e \cdot w \mod n, \quad u_2 = r \cdot w \mod n$$5. **Punktrechnung**  
    - $P = u_1 \cdot G + u_2 \cdot Q = (x_2, y_2)$

5. **Verifikation**  
    - $r = x_2 \mod n$.  
    - Wenn gleich, Signatur ist gültig; sonst ungültig.

## 4. Sicherheit
- **Unumkehrbarkeit** der diskreten Logarithmus‐Aufgabe auf elliptischen Kurven schützt $d$.
- **Schutz gegen Seitenkanal‐Angriffe**: Implementation muss $k$ auf [[HSM]]/Elliptic-Curve-Acceleration hardware ausführen.
- **Random $k$** schützt vor Wiederverwendungslücken.


### Zusammenfassung

> **ECDSA** kombiniert ein **Hash** der Nachricht mit einem **zufälligen Skalar $k$** und den privaten Schlüssel $d$, um zwei Werte $(r, s)$ zu erzeugen, die nur mit dem zugehörigen **öffentlichen Schlüssel $Q$** und denselben Kurvenparametern verifiziert werden können.

So stellt ECDSA **Integrität**, **Authentizität** und **Nicht-Abstreitbarkeit** sicher – bei wesentlich kleineren Schlüsseln und Unterschriften als vergleichbare RSA-Verfahren.