**SSL (Secure Sockets Layer)** ist der Vorläufer des heutigen [[TLS]]-Protokolls und definiert, wie zwei Teilnehmer (z. B. Web-Browser und Server) über ein unsicheres Netzwerk sicher kommunizieren können. Kernprinzip: Aufbau eines verschlüsselten, integritäts­gesicherten „Tunnels“ mit gegenseitiger (oder zumindest einseitiger) Authentisierung.

## 1. Protokollarchitektur

SSL ist in mehrere **Protokollschichten** unterteilt, die aufeinander aufbauen:

1. **SSL Record Protocol**
    - Verantwortlich für Fragmentierung, Kompression (optional), Verschlüsselung und MAC (Message Authentication Code) jeder Nachricht.
    - Kapselt alle höheren Protokolle (Handshake, ChangeCipherSpec, Alert).

2. **Handshake Protocol**    
    - Führt den **Schlüsselaustausch**, die **Authentisierung** und die **Aushandlung von Algorithmen** durch.

3. **ChangeCipherSpec Protocol**    
    - Kurze Nachricht, die signalisiert: „Ab jetzt verwenden wir die vereinbarten Schlüssel und Algorithmen!“

4. **Alert Protocol**    
    - Wird benutzt, um **Fehler** zu melden (z. B. „Bad Certificate“, „Unexpected Message“) oder die Verbindung korrekt zu schließen.



## 2. Ablauf des SSL-Handshakes

1. **ClientHello**    
    - Client sendet:
        - SSL-Version (z. B. SSL 3.0)
        - Zufallszahl (ClientRandom, 32 Byte)
        - Liste unterstützter Cipher-Suites (z. B. RSA-AES256-SHA, DH-DES-MD5)
        - Kompressionsmethoden (meist „null“)

2. **ServerHello**    
    - Server antwortet:
        - Gewählte SSL-Version
        - Zufallszahl (ServerRandom, 32 Byte)
        - Ausgewählte Cipher-Suite
        - Gewählte Kompression

3. **Server Certificate**    
    - Server sendet sein **[[X.509]]-Zertifikat** (Public Key), um sich gegenüber dem Client zu authentisieren.

4. **ServerKeyExchange** (optional)
    - Bei bestimmten Key-Exchange-Algorithmen (z. B. DHE) sendet der Server zusätzliche Parameter (z. B. Diffie-Hellman-Parameter mit digitaler Signatur).

5. **CertificateRequest** (optional)    
    - Server kann den Client zur **Client-Authentisierung** auffordern (Client-Zertifikat).

6. **ServerHelloDone**    
    - Signalisiert dem Client, dass der Server fertig ist mit seinen Handshake-Nachrichten.

7. **Client Certificate** (optional)    
    - Wenn angefordert, schickt der Client sein Zertifikat.

8. **ClientKeyExchange**    
    - Client übermittelt die **Pre-Master-Secret**:
        - Bei **RSA**: Pre-Master verschlüsselt mit dem Server-Public-Key.
        - Bei **Diffie-Hellman**: öffentlicher Part des DH-Schlüsselaustauschs.

9. **CertificateVerify** (optional)    
    - Client signiert Teile des bisherigen Handshakes mit seinem Private Key (nur wenn Client-Zertifikat genutzt wurde).

10. **ChangeCipherSpec (Client → Server)**    
    - Der Client wechselt in den Modus „ab jetzt verschlüsseln wir gemäß den vereinbarten Parametern“.

11. **Finished (Client → Server)**    
    - Eine verschlüsselte, MAC-geschützte Nachricht, die bestätigt, dass der Client alle Handshake-Nachrichten korrekt empfangen und verarbeitet hat (Inhalt = Hash aller bisherigen Handshake-Nachrichten).

12. **ChangeCipherSpec (Server → Client)**    
    - Der Server wechselt ebenfalls in den verschlüsselten Modus.

13. **Finished (Server → Client)**    
    - Entsprechende Bestätigung vom Server.


Nach diesen Schritten haben beide Seiten:
- Ein **gemeinsames Master-Secret**, aus ClientRandom, ServerRandom und Pre-Master-Secret abgeleitet.
- Eine Reihe von **Schlüsseln** für Verschlüsselung (je nach bis zu vier Kanälen), MAC und Initialisierungs-Vektoren.


## 3. Datentransport & Verschlüsselung
- **Verschlüsselung**: Blockchiffren (z. B. [[AES]], 3DES) im CBC- oder GCM-Modus, oder Stromchiffren (z. B. RC4 in älteren Versionen).
- **Integrität**: HMAC (SHA-1 oder [[SHA]]-256) über verschlüsselten Payload.
- **Sequenznummern** und **Padding** sorgen für Schutz gegen Replay- und Padding-Oracle-Angriffe.


## 4. Verbindungsschluss

1. **Close Notify** (Alert-Level)    
    - Eine Seite sendet eine „close_notify“-Alert, um höflich das Ende zu signalisieren.

2. **Close Notify** der Gegenstelle    
    - Die andere Seite antwortet ebenfalls mit „close_notify“.

3. **TCP-Close**    
    - Der darunterliegende [[TCP]]-Socket wird dann sauber heruntergefahren.


## 5. Evolution zu TLS
- **SSL 3.0** war die letzte SSL-Version; **TLS 1.0** (RFC 2246) baute darauf auf und schloss Schwachstellen.
- Seitdem kamen TLS 1.1, 1.2 und das aktuelle **TLS 1.3**, das viele Schritte zusammenfasst (z. B. **0-RTT Handshake**) und veraltete Algorithmen entfernt hat.
- In der Praxis spricht man heute fast ausschließlich von **TLS**, auch wenn in vielen Configs noch „SSL“ steht.


**Zusammenfassung:**  
SSL realisiert über einen mehrstufigen **Handshake** eine **vertrauenswürdige Authentisierung**, handhabt den **Key Exchange** (RSA oder DH), wechselt in einen **verschlüsselten Kanal**, stellt **Daten­integrität** via [[HMAC]] sicher und bietet mit dem **Alert- und ChangeCipherSpec-Protokoll** den sauberen Betrieb und Abschluss einer gesicherten Verbindung.