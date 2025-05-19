**HMAC (Hash-based Message Authentication Code)** ist ein Verfahren, um mit Hilfe einer kryptografischen Hashfunktion (z. B. [[SHA]]-256) **integritäts­geschützte und authentisierte** Nachrichten­prüfsummen zu erzeugen.

## Grundprinzip
1. **Geheimer Schlüssel**  
	- Du hast einen gemeinsamen geheimen Schlüssel **K**, den nur Sender und Empfänger kennen.    

2. **Innerer und äußerer Padding-Block**
    - Lege eine Blockgröße **B** fest (für SHA-256: 64 Byte).
    - Erzeuge zwei Byte-Arrays der Länge B:
        - **i_key_pad** = (K   xor  0x36      …)
        - **o_key_pad** = (K   xor  0x5C      …)  
          (Falls K länger als B ist, wird es zuerst mit der Hashfunktion auf B-Länge “gehasht” (K′ = H(K)); ist K kürzer, wird es mit Nullen aufgefüllt.)

3. **Doppelte Hash-Runde**    
```Text
   inner  = H(i_key_pad  ∥  Nachricht) HMAC   = H(o_key_pad  ∥  inner)
```
- Das erste Hashing bindet den Schlüssel an die Nachricht, das zweite schützt die Zwischensumme vor Angreifern.


## Warum so kompliziert?
- **Sicher gegen Length-Extension-Angriffe**  
    Weil bei Merkle-Damgård-Hashes (z. B. SHA-256) einfache „Hash(K ∥ Nachricht)“-MACs für Angreifer anfällig wären, eine Nachricht zu verlängern und einen gültigen MAC nachzurechnen. HMAC umgeht das durch die doppelte, gepaddete Hash-Runde.
- **Key-Separation**  
    Durch die unterschiedlichen Pads (0x36 vs. 0x5C) werden innerer und äußerer Hash klar voneinander getrennt.
- **Flexibel**  
    HMAC kann mit jeder Block-basierten Hashfunktion genutzt werden (SHA-1, SHA-256, SHA-3 …).

## Pseudocode (SHA-256)
```Python
def HMAC_SHA256(key, message):     
	B = 64  # Byte-Blockgröße für SHA-256     
	if len(key) > B:        
		key = SHA256(key)         # Schritt 1: Kürzen     
	key = key.ljust(B, b'\x00')   # Schritt 2: Auffüllen auf B Bytes      
	o_key_pad = bytes((b ^ 0x5C) for b in key)     
	i_key_pad = bytes((b ^ 0x36) for b in key)      
	inner_hash = SHA256(i_key_pad + message)     
	return SHA256(o_key_pad + inner_hash)
```

## Einsatz in Protokollen
- **[[TLS]]**: zur Nachrichtenauthentifizierung in älteren Versionen (MAC-then-Encrypt)
- **[[IPsec]] (AH)**: Integrity Check Value (ICV) mittels HMAC-SHA1 / HMAC-SHA256
- **[[SSH]]**, **JSON Web Tokens (JWS)**, **REST-APIs**: Signatur von Token oder Payloads

> **Fazit:**  
> HMAC kombiniert die **Geschwindigkeit** von Hashfunktionen mit der **Sicherheit** eines geheimen Schlüssels, liefert so einen robusten Schutz gegen Nachrichtenmanipulation und ist in nahezu allen sicherheitsrelevanten Protokollen unverzichtbar.