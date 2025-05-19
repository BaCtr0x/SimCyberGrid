**ECIES** (Elliptic-Curve Integrated Encryption Scheme), das häufig in IEC-basierten Systemen als **hybrides Verschlüsselungsverfahren** zum Einsatz kommt. ECIES kombiniert **asymmetrische Elliptische-Kurven-Kryptographie** mit **symmetrischer Verschlüsselung** und **MAC** für Vertraulichkeit, Integrität und Authentizität.

## 1. Grundidee
1. **Asymmetrischer Anteil**
    - Einmaliger, zufälliger **Ephemeral-Key** (privater Ephemeral-Schlüssel _r_ und öffentlicher Punkt $R = r\cdot G$) wird erzeugt.
    - Mit dem Empfänger-Static-Key $Q = d\cdot G$ ($d$ = Empfänger-Privat­schlüssel) rechnet der Sender das gemeinsame Geheimnis$$S=r\cdot Q=r\cdot d\cdot G$$
2. **Key-Derivation**
    - Aus _S_ wird über einen **KDF** (z. B. HKDF-SHA-256)
        - ein **Encryption Key (K_E)** und
        - ein **MAC Key (K_M)**  
            abgeleitet.

3. **Symmetrische Verschlüsselung**    
    - Die Nachricht _M_ wird mit einem **AES-GCM**- oder **[[AES]]-CBC+HMAC**-Schema unter _K_E_ verschlüsselt und ergibt den **Ciphertext C**.

4. **Message Authentication Code**    
    - Mit _K_M_ wird über $C$ plus ggf. Zusatzdaten (Associated Data) ein **MAC $T$*** berechnet (z. B. [[HMAC]]-[[SHA]]-256 oder AES-GCM-Tag).

5. **Zusammenbau der Nachricht**    
    - Der Sender überträgt an den Empfänger das Tripel$$\{R, C, T\}$$

## 2. Entschlüsselung beim Empfänger
1. **Shared Secret rekonstruieren**$$S' = d \cdot R = d \cdot (r \cdot G) = r\cdot d\cdot G = S$$
2. **Key-Derivation**  
    - Aus _S'_ werden dieselben _K_E_ und _K_M_ per KDF erzeugt.

3. **MAC-Prüfung**  
    - Mit _K_M_ den empfangenen Tag $T$ überprüfen. Bei Fehlern Abbruch.

4. **Symmetrische Entschlüsselung**  
    - Den Ciphertext $C$ mit _K_E_ entschlüsseln und $M$ gewinnen.


## 3. Vorteile von ECIES
- **Perfect Forward Secrecy** (sofern Ephemeral-Keys einmalig sind).
- **Kleine Schlüssel** (z. B. 256-Bit ECC statt 3072-Bit RSA).
- **Hybrid-Effizienz**: Nur ein kurzer EC-Handshake, dann schnelle symmetrische Krypto.  
- **Integrität & Authentizität** durch [[MAC]]-Tag.    



> **Kurzfassung:**  
> _ECIES ist ein Hybrid-Kryptosystem, bei dem du mit einem einmaligen ECC-Schlüsselaustausch einen symmetrischen Schlüssel ableitest, mit dem du dann deine Nutzdaten sicher per AES verschlüsselst und per MAC absicherst._