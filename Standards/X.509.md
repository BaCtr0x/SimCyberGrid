Ein **X.509-Zertifikat** ist ein standardisiertes Daten­objekt zur **Authentisierung** und **Verteilung öffentlicher Schlüssel** in PKI-Umgebungen (Public Key Infrastructure). Es definiert, **wer** einen bestimmten öffentlichen Schlüssel besitzt und **bis wann** dieses Vertrauen gilt.

### Aufbau eines X.509-Zertifikats
1. **Version**  
    - Meist Version 3; erlaubt Erweiterungen („Extensions“).

2. **Seriennummer**  
	- Eindeutige Kennung, vergeben durch die Zertifizierungsstelle (CA).

2. **Signaturalgorithmus**  
    - z. B. `sha256WithRSAEncryption` oder `ecdsa-with-SHA256`.

3. **Issuer (Aussteller)**  
    - Identität der CA als Distinguished Name (z. B. `CN=MyCA, O=Example Corp, C=DE`).

4. **Gültigkeitsperiode**    
    - **Not Before**: frühestes Datum/Uhrzeit, ab dem das Zertifikat gültig ist.
    - **Not After**: Ablaufdatum/Uhrzeit, nach dem es ungültig wird.

5. **Subject (Inhaber)**  
    - Identität des Zertifikats-Besitzers (Hostnamen, Benutzer, Gerät).

6. **Subject Public Key Info**  
    - Algorithmus und öffentlicher Schlüssel (RSA-Modulus/Exponent oder ECC-Kurve/Punkt).
 
7. **Extensions** (optional, Version 3)    
    - **Key Usage**: wozu der Schlüssel dienen darf (Digital Signature, Key Encipherment, etc.).
    - **Extended Key Usage**: z. B. TLS-Serverauthentifizierung, E-Mail-S/MIME.
    - **Subject Alternative Name**: zusätzliche Namen (DNS, IP, E-Mail).
    - **CRL Distribution Points**: URL(s) zur Sperrliste (CRL).
    - **Authority Information Access**: OCSP-Responder-URL(s).
    - **Basic Constraints**: ob das Zertifikat selbst als CA fungieren darf.

8. **Signature Value**  
    - Die **Signatur** der CA über all die obigen Felder (mit ihrem privaten Schlüssel), um ihre Echtheit und Unversehrtheit zu garantieren.    


### Lebenszyklus

1. **Zertifikatsanforderung (CSR)**  
    - Der Antragsteller erzeugt ein Schlüsselpaar, baut einen _Certificate Signing Request_ mit seinem öffentlichen Schlüssel, unterschreibt diesen und sendet ihn an die CA.

2. **Zertifikatsausstellung**  
    - Die CA prüft Identität/Attribute, signiert das Zertifikat und stellt es aus.

3. **Verteilung**  
    - Das Zertifikat wird an Clients/Server verteilt und üblicherweise in Verzeichnissen (LDAP, HTTP) öffentlich zugänglich gemacht.

4. **Widerruf**  
    - Vor Ablauf kann die CA es widerrufen (etwa bei Schlüssel­kompromittierung). Der Widerrufs­status ist über **[[CRL]]** oder **[[OCSP]]** abrufbar.


### Einsatzgebiete
- **[[TLS]]/[[SSL]]** für HTTPS, MQTT, OPC UA usw.
- **Code Signing** von Software-Paketen.
- **E-Mail-S/MIME** zur Signatur/Verschlüsselung.
- **Client-Authentifizierung** (z. B. SMGW-TLS mit gegenseitiger Authentisierung).


> **Kurz:**  
> _Ein X.509-Zertifikat verknüpft einen öffentlichen Schlüssel mit einer definierten Identität (Host, Benutzer, Gerät), von einer vertrauenswürdigen CA signiert und mit Gültigkeits­zeitraum sowie Erweiterungen versehen._