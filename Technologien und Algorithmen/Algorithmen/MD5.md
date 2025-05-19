**MD5 (Message‐Digest Algorithm 5)** ist eine weit verbreitete kryptografische Hashfunktion, die eine **beliebig lange** Eingabebotschaft auf einen **128 Bit** (16 Byte) langen Fingerabdruck (Digest) abbildet. Obwohl MD5 heute als unsicher gilt (Kollisions­angriffe möglich), sei hier das Grundprinzip erläutert:

## 1. Merkle-Damgård-Konstruktion & Padding

1. **Padding**    
    - Die Nachricht wird so aufgefüllt, dass ihre Länge (in Bits) ≡ 448 mod 512 wird:
        - Ein “1”-Bit, gefolgt von so vielen “0”-Bits, bis noch 64 Bit Platz bleiben.
    - In den letzten 64 Bits wird die **ursprüngliche Nachrichtenlänge** (vor Padding) als 64-Bit-Little-Endian-Wert angehängt.

2. **Blockbildung**    
    - Die gepaddete Nachricht wird in **512 Bit-Blöcke** (16 Worte zu je 32 Bit) zerlegt.


## 2. Initialisierung

- Es gibt vier 32-Bit-Register **A, B, C, D** mit festen Anfangswerten (in hexadezimal):    
```mathematica
A₀ = 0x67452301   
B₀ = 0xEFCDAB89   
C₀ = 0x98BADCFE   
D₀ = 0x10325476
```

## 3. Hauptschleife: 4 Runden à 16 Schritte

Für jeden 512 Bit-Block Mᵢ:
1. **Kopie der Register**
```mathematica
A = A₀,
B = B₀,
C = C₀,
D = D₀
```    

2. **Vier nicht-lineare Funktionen**    
    - **F**(B,C,D) = (B ∧ C) ∨ (¬B ∧ D)
    - **G**(B,C,D) = (B ∧ D) ∨ (C ∧ ¬D)
    - **H**(B,C,D) = B ⊕ C ⊕ D
    - **I**(B,C,D) = C ⊕ (B ∨ ¬D)

3. **Runden-Schritt**  
    Für **j = 0 … 15** in Runde 1, **j = 16 … 31** in Runde 2, etc.:
```python
F_j = [F, G, H, I] abhängig von der Runde 
K_j = vorgegebene 32-Bit-Konstante = ⌊|sin(j+1)|·2³²⌋ 
s_j = runde-abhängiger Shift-Offset aus Standardtabelle  
Temp = D 
D = C 
C = B 
B = B +  ((A + F_j(B,C,D) + Mᵢ[k_j] + K_j) <<< s_j)
A = Temp
```
    
- `<<< s` ist die zyklische Links-Rotation um s Bit.
- `k_j` ist eine Block-Byte-Index-Reihenfolge, die je Runde variiert.

4. **Hinzufügen zur Akkumulation**  
    Nach 64 Schritten:
```mathematica
A₀ = A₀ + A   
B₀ = B₀ + B   
C₀ = C₀ + C   
D₀ = D₀ + D
```


## 4. Ausgabe
- Nach Verarbeitung aller Blöcke wird der 128 Bit-Digest als **A₀‖B₀‖C₀‖D₀** (je 32 Bit, Little-Endian) ausgegeben.


## 5. Eigenschaften & Sicherheit
- **Avalanche-Effekt:** Kleine Eingabeänderung → völlig anderer Digest.
- **Kollisionsanfälligkeit:** MD5 ist heute **nicht mehr collision-resistent**; praktische Kollisionen (zwei verschiedene Nachrichten mit gleichem Hash) sind möglich.
- **Performance:** Sehr schnell in Software, daher noch in manchen Legacy-Systemen verwendet.

### Kurzzusammenfassung

1. **Pre-Processing:** Padding (1 Bit + 0-Bits + Längenfeld) → 512 Bit-Blöcke.
2. **Initialisierung:** Vier 32 Bit-Register mit festen Werten.
3. **Compression Loop:** 4 Runden × 16 Schritte mit Funktionen F, G, H, I, vordefinierten Konstanten, Bit-Rotationen.    
4. **Finalisierung:** Additive Akkumulation der Register → 128 Bit Hash.


> **Merksatz:**  
> _MD5 ist ein Merkle-Damgård-Hash mit 512 Bit-Blöcken und vier Runden Feistel-ähnlicher Verarbeitung, das am Ende 128 Bit Digest liefert – heute jedoch kryptografisch überholt._