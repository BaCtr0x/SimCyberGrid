**DES (Data Encryption Standard)** ist ein symmetrisches Blockchiffre-Verfahren, das auf einem **Feistel-Netzwerk** mit 16 Runden basiert. Hier die wesentlichen Schritte und Komponenten:

## 1. Block- und Schlüssellänge
- **Blockgröße:** 64 Bit
- **Hauptschlüssel:** 56 Bit wirksam + 8 Paritäts-Bits (jeweils ein Paritäts-Bit pro Byte)


## 2. Initial- und Final-Permutation
1. **IP (Initial Permutation):** Vertauscht die Bit-Positionen des 64-Bit-Blocks nach einer festen Tabelle.
2. **FP (Final Permutation):** Wendet nach den 16 Runden die **inverse** Permutation von IP an, um den verschlüsselten Block zu erzeugen.

Diese Permutationen haben keine kryptographische Stärke, sie verteilen nur Bits vor und nach den Runden.

## 3. Feistel-Netzwerk
Nach IP wird der Block in **je 32 Bit** geteilt („Left“ L₀, „Right“ R₀). Dann folgen 16 identische Runden mit jeweils:
```R
L_i = R_{i-1}
R_i = :_{i-1} XOR F(R_{i-1}, K_i)
```

- bitweises XOR, K_i = Rundenschlüssel der Runde i.



## 4. Rundefunktion F

Für jede Runde i berechnet F folgende Schritte:
1. **Expansion (E):** Dehnt R_{i-1} von 32 auf 48 Bit aus, indem bestimmte Bits dupliziert werden, um zu Kᵢ passen zu können.
2. **Key Mixing:** XOR von 48 Bit Expanded-R und 48 Bit Rundenschlüssel K_i.
3. **Substitution (S-Boxen):** Teilt das 48 Bit-Ergebnis in 8 Blöcke zu je 6 Bit. Jeder 6-Bit-Block wird durch eine der 8 vordefinierten **S-Boxen** (je 4 Zeilen×16 Spalten) auf 4 Bit abgebildet. Dadurch entsteht 32 Bit.
4. **Permutation (P):** Verteilt die 32 Bit über neue Positionen gemäß einer festen P-Tabelle, um die Diffusion weiter zu erhöhen.


## 5. Schlüssel-Schedule

Aus dem 56 Bit-Hauptschlüssel werden 16 Rundenschlüssel Kᵢ à 48 Bit erzeugt:
1. Paritäts-Bits entfernen → 56 Bit.
2. **Permuted Choice 1 (PC-1):** Permutation und Aufteilung in zwei 28-Bit-Hälften (C₀, D₀).
3. Für jede Runde i:
    - Linke Rotationen von Cᵢ₋₁, Dᵢ₋₁ um 1 oder 2 Bit (abhängig von i) → Cᵢ, Dᵢ.
    - **Permuted Choice 2 (PC-2):** Auswahl und Permutation von 48 Bit aus Cᵢ∥Dᵢ → Kᵢ.


## 6. Entschlüsselung

Wird durch **gleiche Architektur** erreicht – nur werden die Rundenschlüssel **in umgekehrter Reihenfolge** (K₁₆ bis K₁) eingesetzt. Weil es ein Feistel‐Netzwerk ist, braucht der Algorithmus selbst keine Änderung.


## 7. Betriebsmodi

Da DES nur 64 Bit auf einmal chiffriert, nutzt man Modi wie:
- **ECB (Electronic Codebook)** – unabhängige Blöcke (nicht empfohlen).
- **CBC (Cipher Block Chaining)** – jeder Block wird mit Ciphertext des Vorblocks XOR-verknüpft.
- **CFB, OFB, CTR** – strömungsorientierte Modi für unterschiedlichen Sicherheit/Leistungsausgleich.


## 8. Sicherheit & Nachfolger
- **Schlüssellänge 56 Bit** gilt heute als **brute-force-angreifbar**.
- **3DES** kombiniertes Verfahren (DES-EDE mit drei 56 Bit-Schlüsseln) ist inzwischen Standardersatz, bis **[[AES]]** übernommen wurde.


> **Kurz:**  
> _DES teilt 64 Bit-Blöcke auf, permutiert sie vorab, verarbeitet sie 16 Runden in einem Feistel-Netzwerk mit Expansion, S-Boxen und Permutationen unter Verwendung rotierender Schlüssel und permutiert dann abschließend zurück._