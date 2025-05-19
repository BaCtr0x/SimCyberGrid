**SHA (Secure Hash Algorithm)** ist eine Familie kryptografischer **Einweg-Hashfunktionen**, die beliebige Eingabedaten auf einen **festen Ausgabe-(Digest-)Wert** („Fingerprint“) abbildet. Wichtige Eigenschaften sind:

1. **Deterministisch & Eingabelänge-unabhängig**    
    - Egal wie groß die Eingabe (Text, Datei, beliebige Bits) ist – das Ergebnis (z. B. 256 Bit bei SHA-256) hat immer dieselbe Länge.
    - Dieselbe Eingabe → immer derselbe Hash.

2. **Einweg & Kollisionsresistenz**    
    - Aus dem Hash lassen sich (praktisch) **nicht** die ursprünglichen Daten rekonstruieren.
    - Es ist (praktisch) **unmöglich**, zwei verschiedene Eingaben mit demselben Hash zu finden (Kollision).

3. **Avalanche-Effekt**    
    - Schon eine einzelne Bitänderung in der Eingabe führt zu einem völlig anderen Hash (50 % der Ausgabebits kippen im Mittel).


## SHA-2 (z. B. SHA-256/SHA-512, FIPS 180-4)

1. **Padding & Parsing**    
    - Die Eingabe wird auf ein Vielfaches der Blockgröße (512 Bit bei SHA-256, 1024 Bit bei SHA-512) aufgefüllt:
        - Ein `1`-Bit, dann so viele `0`-Bits, bis am Ende 64 Bit (bzw. 128 Bit) Länge-Feld Platz haben.
        - Am Ende wird die ursprüngliche Nachrichtenlänge angehängt.

2. **Initialisierung**    
    - Ein Satz von **Initial-Kettenwerten** (8 Wörter bei SHA-256, 8 oder 16 bei SHA-512) wird aus festen Konstanten abgeleitet.

3. **Block-Verarbeitung (Compression-Funktion)**  
    Für jeden Datenblock (512 / 1024 Bit):    
    - **Message Schedule**: Erweiterung des Blocks auf 64 / 80 Sub-Wörter via bitwise Rotation, Shift und Add.
    - **Runden**: 64 / 80 Runden jeweils mit:
        1. **Ch / Maj** (bitweise Auswahl bzw. Mehrheit)
        2. **BigSigma / SmallSigma** (bitweise Rotationen & Shifts)
        3. **AddRoundConstant** (vorgegebene 32‐/64‐Bit Konstante)
        4. **Modular Addition** aller Obigen mit den Arbeitsregistern
    - **Kettenwert-Update**: Die 8 Arbeitsregister werden auf die Kettenwerte addiert.

4. **Ausgabe**
    - Nach allen Blöcken wird der finale Kettenwert als 256 / 512 Bit Hash ausgegeben.

## SHA-3 (Keccak, FIPS 202)

1. **Sponge-Funktion**    
    - **Absorb**: Eingabe wird in **Rate-Chunks** (z. B. 1088 Bit bei SHA-3-256) XOR‐verknüpft mit einem internen **State** (1600 Bit), dann **Permutation** (Keccak-f) angewandt, und so weiter.
    - **Squeeze**: Nach Absorption werden Hash-Bits aus dem State „ausgequetscht“.

2. **Permutation (Keccak-f)**  
    Mehrere Runden von **θ, ρ, π, χ, ι** – bitweise Permutationen, Rotationen und nichtlineare Mischungen.
   
3. **Vorteile gegenüber Merkle-Damgård (SHA-2)**    
    - Kein Length-Extension-Angriff möglich.
    - Flexible Rate-Kapazität-Einteilung: gute Performance auf Hardware und aufkleiner Ressourcen.

### Anwendungsszenarien
- **Integritätsprüfung**: Verifizieren, dass Dateien oder Nachrichten nicht verändert wurden.
- **Passwort-Hashing** (in Kombination mit Salt und iterativem Key-Stretching).
- **[[HMAC]]** (Hash-based Message Authentication Code) zur Gewährleistung von Authentizität und Integrität.
- **Digitale Signaturen**: Der Hash einer Nachricht wird signiert, nicht die ganze Nachricht.

> **Essenz:**  
> SHA-Familien verwandeln **beliebig lange** Daten in **feste, schwer zu fälschende** Digests. SHA-2 setzt auf eine **Merkle-Damgård-Konstruktion** mit Runden-Kompression, SHA-3 nutzt eine **Sponge-Architektur** für mehr Flexibilität und Sicherheit gegen Extensions.