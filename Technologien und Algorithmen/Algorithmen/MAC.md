Ein **MAC** (Message Authentication Code) ist eine kurze Prüfsumme, die mit einem **geheimen Schlüssel** über eine Nachricht berechnet wird, um gleichzeitig **Integrität** und **Authentizität** sicherzustellen.

## 1. Grundprinzip
1. **Geheimer Schlüssel**  
    Sowohl Sender als auch Empfänger teilen sich einen symmetrischen Schlüssel **K**.

2. **MAC-Berechnung**  
    Eine Funktion `MACₖ(M)` nimmt als Eingabe die Nachricht **M** und den Schlüssel **K** und liefert einen festen Ausgabewert **T** (den Tag) – typischerweise 64 … 256 Bit lang.    

3. **Nachrichtenaufbau**  
    Der Sender schickt:
```r
M || T
```   
3. **Prüfung beim Empfänger**
    - Empfänger erhält `M' | T'`.
    - Er berechnet `T-berechnet = MAC_k(M')`.
    - Vergleicht `T-berechnet == T'`.
        - **Ja** → Nachricht ist unversehrt und stammt vom Schlüsselinhaber.
        - **Nein** → Integritätsverletzung oder Fälschungsversuch.

## 2. Typische MAC-Verfahren

| Verfahren   | Grundidee                                     | Einsatzbeispiel                  |
| ----------- | --------------------------------------------- | -------------------------------- |
| **HMAC**    | Hash-basierter MAC ([[SHA]]-Family + Key-Pad) | [[TLS]], REST-APIs, Web-Tokens   |
| **CMAC**    | Block-Cipher-MAC (z. B. AES-CMAC)             | Smart-Cards, IEEE-802.11i        |
| **GMAC**    | Galois/Counter-Mode MAC (AES-GCM ohne IV-Tag) | [[IPsec]] ESP, WLAN (WPA2)       |
| **CBC-MAC** | CBC-Mode über Blöcken, letzter Block als Tag  | ältere Protokolle, eingeschränkt |

---

## 3. Beispiel: AES-CMAC (kurz)

1. **Subkeys generieren** aus **K** via AES auf Null-Block.
2. **Nachricht in Blocklängen** (128 Bit) aufteilen, ggf. mit Padding.
3. **CBC-Verschlüsselung**:
```makefile
X_0 = 0^128
for i=1...128:
	X_i = AES_k(M_i XOR X_{i-1})
Tag = X_n
```
4. **Tag** wird an M angehängt.


## 4. Eigenschaften & Sicherheit
- **Integrität**: Jede Bitänderung in M ➔ falscher Tag.
- **Authentizität**: Nur wer K kennt, kann gültigen T erzeugen.
- **Einweg-Charakter**: Aus T lässt sich weder M noch K rekonstruieren.
- **Collision-Resistance**: Ohne K praktisch unmöglich, zwei verschiedene Nachrichten mit demselben Tag zu finden.


### Merksatz

> _Ein MAC ist wie eine digitale Unterschrift aus einem gemeinsamen Geheimnis – er garantiert, dass die Nachricht weder verändert noch von Unbefugten erzeugt wurde._