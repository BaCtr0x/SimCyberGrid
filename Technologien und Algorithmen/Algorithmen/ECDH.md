**ECDH (Elliptic-Curve Diffie-Hellman)** ist ein Verfahren zum **sicheren Schlüsselaustausch** über ein unsicheres Netzwerk, das die Mathematik elliptischer Kurven nutzt, um aus je zwei privaten Schlüsseln einen **gemeinsamen geheimen Schlüssel** (Shared Secret) abzuleiten – ohne dass der Schlüssel selbst je über das Netz übertragen wird.

## 1. Grundlagen elliptischer Kurven
1. **Kurvengleichung**  
    Eine elliptische Kurve über einem endlichen Feld 𝐹ₚ (p-Primzahl) hat die Form
   $$y2=x3+ax+b\mod p$$
	 wobei die Koeffizienten a, b so gewählt sind, dass die Kurve keine Singularitäten hat (Diskriminante ≠ 0).    
2. **Gruppenstruktur**  
    Die Punkte (x,y) auf der Kurve plus ein „Nullpunkt“ 𝒪 bilden eine abelsche Gruppe. Punktaddition und -verdopplung definieren die Gruppenoperation.
3. **Generatorpunkt G**  
    Für eine gegebene Kurve wählt man öffentlich einen festgelegten Punkt G, dessen Ordnung n eine große Primzahl ist.

## 2. Schlüsselerzeugung
Jeder Teilnehmer erzeugt sein Schlüsselpaar:
1. **Privater Schlüssel**  
    - Zufällige $𝑑 \in [1, n–1]$
2. **Öffentlicher Schlüssel**  
    - Punktmultiplikation: $𝐐 = 𝐝 \cdot 𝐆$  
    - $𝐐$ ist ein Punkt $(x, y)$ auf der Kurve und wird öffentlich kommuniziert.

## 3. Gemeinsamen Schlüssel ableiten
Angenommen Alice und Bob wollen einen gemeinsamen Schlüssel:
1. **Alice** wählt $𝑑_a$, berechnet $Q_a = d \cdot G$ und sendet $Q_a$ an Bob.
2. **Bob** wählt $𝑑_{b}$, berechnet $𝐐_b = 𝑑_b \cdot G$ und sendet $𝐐_b$ an Alice.
3. **Alice** berechnet $𝑑_a \cdot𝐐_b = 𝑑_a \cdot(𝑑_b\cdot G) = (𝑑_a\cdot𝑑_b\cdot·G$.
4. **Bob** berechnet $𝑑_b\cdot 𝐐_a = 𝑑_b\cdot (𝑑_a \cdot G) = (𝑑_b\cdot 𝑑_a)\cdot G$.

Da Multiplikation kommutativ ist, erhalten beide denselben Kurvenpunkt $𝐊 = (𝑑_a \cdot 𝑑_b)\cdot G$. Aus einer Koordinate (z. B. $x$) oder mittels Hashing dieses Punktes lässt sich dann ein symmetrischer Sitzungsschlüssel ableiten.

## 4. Sicherheit
- **Diskrete Logarithmus­schwierigkeit**: Aus $𝐊_a = 𝑑\cdot G$ lässt sich 𝑑 nicht effizient berechnen, wenn die Kurve und $n$ groß genug gewählt sind (z. B. secp256r1 mit $n \approx 2^{256}$).
- **Perfect Forward Secrecy**: Bei jedem Handshake werden neue Zufalls $𝑑_a/𝑑_b$ gewählt, so dass eine spätere Kompromittierung eines Schlüssels nicht frühere Sitzungen gefährdet.

## 5. Einsatz in TLS
1. **ClientHello** und **ServerHello** terminieren:  
    - Kurvenparameter und bevorzugte KEX-Methode (ECDHE) werden ausgehandelt.

2. **ServerKeyExchange**  
    - Server sendet seinen öffentlichen Schlüssel $𝐐_s = 𝑑_s \cdot G$ und ggf. eine Signatur über $𝐐_s$.
   
3. **ClientKeyExchange**  
    - Client sendet seinen öffentlichen Schlüssel $𝐐_c = 𝑑_c\cdot G$.

4. **Shared Secret**  
    - Beide Seiten berechnen $(𝑑_c\cdot 𝐐_s)$ bzw. $(𝑑_s \cdot 𝐐_c)$.
   
5. **Master Secret**  
    - Aus dem gemeinsamen Punkt wird über ein KDF der symmetrische [[TLS]]-Schlüssel abgeleitet.


---

### Fazit

> **ECDH** ermöglicht zwei Parteien, **ohne direkte Übertragung** eines gemeinsamen Schlüssels einen sicheren Sitzungsschlüssel abzuleiten, basierend auf der **unpraktisch schwierigen** elliptischen Kurven-Diskreten-Logarithmus-Aufgabe.