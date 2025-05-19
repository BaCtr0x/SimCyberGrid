**SSH (Secure Shell)** ist ein Netzwerkprotokoll, das einen **sicheren, verschlüsselten Kanal** zwischen einem SSH-Client und einem SSH-Server über ein unsicheres Netzwerk (z. B. das Internet) herstellt. Es kombiniert **Authentifizierung**, **Vertraulichkeit**, **Integrität** und **Tunnel-Funktionalität**. Im Folgenden die wesentlichen Bestandteile und Abläufe:

## 1. Architektur & Schichten

SSH gliedert sich in drei Haupt­schichten:
1. **Transport Layer Protocol**
    - Stellt die **sichere Verbindung** her: Verschlüsselung (Symmetrisch), Integritäts­prüfung (MAC/HMAC), optionale Server-Authentisierung per Host-Key.
    - Verantwortlich für das **Key Exchange** (Schlüsselaustausch) und das **Session-Setup**.

2. **User Authentication Protocol**    
    - Authentisiert den Benutzer gegenüber dem Server:
        - **Passwort**
        - **Public-Key** (Schlüssel­paare, die auf dem Server als autorisierte Keys hinterlegt sind)
        - **Keyboard-Interactive**, **GSSAPI**, **Host-based**, etc.

3. **Connection Protocol**    
    - Ermöglicht mehrere **virtuelle Kanäle** („channels“) über dieselbe TCP-Verbindung:
        - Terminal-Shell (interactive shell)
        - SFTP-Subsystem
        - TCP-Forwarding (Port-Forwarding)
        - X11-Forwarding


## 2. Verbindungsaufbau & Key Exchange
1. **TCP-Verbindung zu Port 22**
    - Client öffnet TCP-Socket zum SSH-Server (Default Port 22).

2. **Server Identification**    
    - Server sendet seine **Host-Key** (Public Key) und listet unterstützte Verschlüsselungs- und MAC-Algorithmen.

3. **Algorithmen-Aushandlung**    
    - Client wählt (aus dem Server-Angebot) die Cipher-Suite, MAC-Algorithmus und Kompressions­option aus und bestätigt das.

4. **Key Exchange (Diffie-Hellman / ECDH)**    
    - Client und Server führen einen **Diffie-Hellman- oder ECDH-Austausch** durch, um einen gemeinsamen **Session-Schlüssel** zu berechnen, ohne dass dieser über das Netz übertragen wird.
    - Aus diesem Session-Key leiten beide Seiten symmetrische Schlüssel (für Verschlüsselung und MAC) ab.

5. **Integrity & Encryption Activation**    
    - Sobald der Schlüssel etabliert ist, werden alle folgenden SSH-Pakete symmetrisch verschlüsselt und mit HMAC versehen.


## 3. Benutzer-Authentifizierung
1. **„Userauth Request“**
    - Innerhalb des sicheren SSH-Transports fordert der Client den Server auf, eine Authentifizierung durchzuführen.

2. **Methoden**    
    - **password**: Client sendet Passwort (verschlüsselt)
    - **publickey**: Client belegt, dass er den Private Key zu einem auf dem Server hinterlegten Public Key besitzt, mittels Signatur einer Server-Challenge
    - **keyboard-interactive**: Mehrstufige Challenge/Response (z. B. OTP, CAPTCHA)
    - **hostbased**: Authentifizierung basierend auf Client-Host and Client-Key

3. **Server-Entscheidung**    
    - Server akzeptiert oder verweigert auf Basis der hinterlegten `~/.ssh/authorized_keys` oder `/etc/ssh/passwd`.

## 4. Virtuelle Kanäle („Channels“)

Nach erfolgreicher Authentifizierung eröffnet der SSH-Client über das Connection Protocol **Channel-Requests**:

|Channel-Typ|Zweck|
|---|---|
|**session**|interaktive Shell, Ausführen von Kommandos|
|**exec**|Einmaliges Ausführen eines spezifischen Befehls|
|**subsystem**|z. B. Start eines SFTP-Subsystems (`sftp`)|
|**direct-tcpip**|Lokales Port-Forwarding: Client → Remote-Netzwerk|
|**forwarded-tcpip**|Remote Port-Forwarding: Server → Client|
|**x11**|X11-Forwarding für GUI-Weiterleitung|

Jeder Channel wird mit einer **Channel-ID** referenziert und multiplex-überlagert über dieselbe zugrunde liegende [[TCP]]-Verbindung. Paketgrößen und Fensterkontrolle (`window size`) sorgen für Fluss- und Staukontrolle.


## 5. Vertraulichkeit & Integrität
- **Verschlüsselung**: Symmetrisches AES, ChaCha20, 3DES, …
- **MAC**: [[HMAC]]-[[SHA]]2, HMAC-SHA1, UMAC, …
- **Optionale Kompression**: z. B. **zlib**, um Bandbreite zu sparen.

Alle Datenpakete tragen am Anfang eine **Länge**, den **Payload** (Daten) und einen **MAC**, womit weder Inhalte noch Reihenfolge unbemerkt manipuliert werden können.

## 6. Verbindungsabbau
1. **Channel Close**
    - Jeder virtuelle Channel wird separat mit einer `channel close`-Nachricht beendet.

2. **Disconnect**    
    - Client oder Server senden eine `SSH_MSG_DISCONNECT`, oft mit Code und Grundtext, und schließen dann die TCP-Verbindung.


### Zusammenfassung

> _SSH baut auf TCP auf und sichert die ganze Kommunikation durch symmetrische Verschlüsselung und HMAC-Integritätschecks. Nach einem Diffie-Hellman-Key-Exchange authentifiziert sich der Nutzer (Password oder Public Key) und eröffnet beliebig viele virtuelle Kanäle (Shell, SFTP, Forwarding) über eine einzelne, stets verschlüsselte Verbindung._