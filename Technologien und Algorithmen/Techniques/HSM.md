**HSM (Hardware Security Module)**  
Ein **HSM** ist ein physischer, manipulations­geschützter Rechner (meist als PCIe-Karte oder Netzwerk-Appliance), der **Kryptografische Operationen** sicher ausführt und **Private Keys** nie unverschlüsselt freigibt.

- **Kernfunktionen**  
    - **Key Management:** Erzeugung, Speicherung und Backup von Schlüsselpaaren (RSA, ECC). 
    - **Krypto-Operationen:** Signieren, Entschlüsseln, Hashing – immer innerhalb des HSM. 
    - **Tamper-Evident & Tamper-Resistant:** Physische Hüllen und Sensoren detektieren und verhindern Manipulationsversuche.
    
- **Interfaces**  
	- PKCS#11 (API für Software) 
	- KMIP (Key Management Interoperability Protocol) 
    - Proprietäre HSM-APIs
    
- **Warum nutzen?**  
    - Schutz vor Diebstahl oder Extraktion von Schlüsseln 
    - Compliance-Anforderungen (z. B. FIPS 140-2 Level 3/4) 
    - Performance-Boost für Hochlast-Signaturen (z. B. TLS-Server mit Millionen Verbindungen)