**OCSP (Online Certificate Status Protocol)** ist ein Internet-Standard (RFC 6960), mit dem Clients in Echtzeit den Widerrufs­status eines [[X.509]]-Zertifikats abfragen, ohne komplette [[CRL]]s herunterladen zu müssen. So funktioniert es Schritt für Schritt:

## 1. Rollen und Komponenten
1. **OCSP-Client** (z. B. Browser, SMGW-Software)
2. **OCSP-Responder** (Dienst der Zertifizierungsstelle, CA)
3. **CA-Zertifikat** und **Responder-Signatur­schlüssel**

Der OCSP-Responder hält eine aktuelle Datenbank der zurückgerufenen Zertifikate der CA.


## 2. Anfrage-Antwort-Ablauf
1. **Request-Erstellung**
    - Client liest aus dem zu prüfenden Zertifikat die Felder **Issuer Name Hash**, **Issuer Key Hash** und **Serial Number**.
    - Baut daraus einen **OCSPRequest** im ASN.1-Format, enthält typischerweise auch einen **Nonce** (Zufallswert) zur Verhindern von Replay-Attacken.

2. **Request-Übertragung**    
    - Client sendet die OCSPRequest per HTTP POST (manchmal GET mit Base64 in URL) an die im Zertifikat unter „Authority Information Access (AIA)“ hinterlegte OCSP-URL.

3. **Responder-Verarbeitung**    
    - Der OCSP-Responder vergleicht die Anfrage mit seiner Widerrufs­liste.
    - Er erzeugt einen **OCSPResponse**, signiert ihn mit seinem privaten Schlüssel (Responder-Signing-Key), und enthält für jede abgefragte Seriennummer einen Status:
        - **good** (gültig)
        - **revoked** (zurückgerufen) inkl. Rückruf-Zeitstempel und ggf. Grund
        - **unknown** (nicht von dieser CA ausgestellt)

4. **Response-Übertragung**    
    - Responder sendet die signierte OCSPResponse zurück an den Client.

5. **Client-Verifikation**    
    - Client prüft:
        1. Signatur auf der Response gegen den Responder-Public-Key (oder gegen’s CA-Zertifikat, wenn Responder-Key darin referenziert wird).
        2. dass der im Response gelieferte Nonce mit dem in der Anfrage übereinstimmt (Schutz gegen Replay).
        3. das Zeitfenster der Response (gültig ab / gültig bis).
    - Dann verwendet er den Status in seiner endgültigen Entscheidung, ob die TLS-Verbindung erlaubt wird oder nicht.


## 3. OCSP Stapling ([[TLS]] Extension RFC 4366)

Um **Leistung** zu verbessern und die **Privatsphäre** des Clients zu schützen, gibt es OCSP-Stapling:
1. **Server-Stapling**
    - Der Web-/Mail-Server fragt periodisch selbst beim OCSP-Responder an und cached die signierte Antwort.
    - Beim TLS-Handshake sendet der Server dem Client die bereits erhaltene OCSPResponse im **CertificateStatus**-Feld.

2. **Vorteile**    
    - **Keine direkten OCSP-Anfragen** des Clients → schneller, weniger Latenz
    - **Datenschutz**: CA erfährt nicht, welcher Client welche Seite anfragt


## 4. Vorteile & Einschränkungen

| Vorteil                                | Einschränkung                                   |
| -------------------------------------- | ----------------------------------------------- |
| Echtzeit-Statusabfrage ohne große CRLs | Benötigt Verfügbarkeit des OCSP-Responders      |
| Geringe Bandbreite durch Einzelanfrage | Einzelne Request→Single Point of Failure        |
| Stapling minimiert Client-Traffic      | Stapled-Response hat begrenzte Gültigkeitsdauer |

---

**Merksatz:**

> _OCSP ist ein leichtgewichtiges, signiertes Frage-Antwort-Protokoll über HTTP, mit dem Clients blitzschnell den Widerrufsstatus einzelner Zertifikate prüfen – und durch OCSP-Stapling sogar ohne eigenen Netzwerk-Call._