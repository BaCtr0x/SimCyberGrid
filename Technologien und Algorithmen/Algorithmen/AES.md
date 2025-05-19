**AES (Advanced Encryption Standard)** ist ein symmetrischer Block­chiffre-Algorithmus, der in einem **Substitutions-Permutations-Netzwerk** (SPN) aufgebaut ist. Er arbeitet auf **128 Bit-Blöcken** und kennt drei Schlüssel­längen: **128, 192 oder 256 Bit**, was zu **10, 12 bzw. 14 Runden** führt.
## 1. Grundaufbau
1. **Blockgröße:** 128 Bit
2. **Schlüssellängen:** 128 / 192 / 256 Bit
3. **Rundenanzahl:**
    - 10 Runden bei 128-Bit-Key
    - 12 Runden bei 192-Bit-Key
    - 14 Runden bei 256-Bit-Key

Jede Runde besteht aus **vier Kernschritten** (außer der letzten, die das MixColumns weglässt):

java

CopyEdit

```Java
State ← AddRoundKey(State, RoundKey[i]) 
For r = 1 to Nr-1:     
	State ← SubBytes(State)
	State ← ShiftRows(State)     
	State ← MixColumns(State)     
	State ← AddRoundKey(State, RoundKey[r]) 
// Letzte Runde: 
State ← SubBytes(State) 
State ← ShiftRows(State) 
State ← AddRoundKey(State, RoundKey[Nr])
```

## 2. Komponenten im Detail
### 2.1 State
Der 128 Bit-Block wird als **4×4-Byte-Matrix** („State“) organisiert:

css

CopyEdit

```CSS
[ b0  b4  b8  b12 ] 
[ b1  b5  b9  b13 ] 
[ b2  b6  b10 b14 ] 
[ b3  b7  b11 b15 ]
```

### 2.2 AddRoundKey

**XOR** des aktuellen State mit dem Rundenschlüssel (je 128 Bit) aus dem **Key–Schedule**.

### 2.3 SubBytes

Nicht-lineare Substitution jedes Bytes über eine **S-Box** (8 → 8 Bit), konstruiert aus dem multiplikativen Inversen in GF(2⁸) plus affiner Transformation. Das sorgt für **Konfusion** (Shannon).

### 2.4 ShiftRows

Zyklisches Verschieben der State-Zeilen um unterschiedliche Offsets:
- Zeile 0: 0 Bytes
- Zeile 1: 1 Byte nach links
- Zeile 2: 2 Bytes
- Zeile 3: 3 Bytes  
    Das trennt die Spalten und erhöht **Diffusion**.

### 2.5 MixColumns

Lineare Transformation jeder Spalte als Polynom-Vielglied in GF(2⁸) multipliziert mit festem Generator-Polynom (0x02,0x03,…). Sorgt weiter für **Diffusion** über Bytes hinweg.

## 3. Key Schedule (Rundenschlüssel-Erzeugung)
1. **Initial Key** wird in 4 Wörter (32 Bit) aufgeteilt.

2. Für jede Runde wird ein neues Wort erzeugt:
    - **RotWord**: rotieren um ein Byte
    - **SubWord**: S-Box-Transformation
    - XOR mit **Rcon**-Konstanten und vorherigem Wort

3. Je nach Key-Länge entstehen so 44 (AES-128), 52 (AES-192) oder 60 (AES-256) 32-Bit-Wörter.    

## 4. Verschiedene Betriebsmodi

Da AES ein reiner Blockchiffre ist, nutzt man **Modi**, um längere Datenströme zu verschlüsseln:
- **ECB** (Electronic Codebook): einfache Block-für-Block-Verschlüsselung (nicht empfohlen)
- **CBC** (Cipher Block Chaining): XOR mit vorherigem Chiffre-Block
- **CTR** (Counter Mode): keystream-basiert, parallelisierbar
- **GCM** (Galois/Counter Mode): kombiniert CTR mit Authentifizierung (AEAD)

## 5. Sicherheit & Einsatz
- **Krypto-Resistenz:** Keine praktischen Angriffe gegen vollen AES-128 bekannt.
- **Hardware-Beschleunigung:** AES-NI in modernen CPUs, spezielle AES-Beschleuniger in HSMs.
- **Weit verbreitet:** Standard in [[TLS]], [[IPsec]], WLAN (WPA2), Secure Storage, Smartcards.

> **Fazit:**  
> AES kombiniert **subtile nicht-lineare Substitution** mit **starker lineare Diffusion** über mehrere Runden und einen ausgeklügelten Key-Schedule, um Datenblöcke sicher und performant zu verschlüsseln.