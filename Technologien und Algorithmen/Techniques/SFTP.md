**SFTP (SSH File Transfer Protocol)** ist ein Dateitransfer-Subsystem, das **über einen bestehenden SSH-Tunnel** läuft. Im Unterschied zu FTPS (FTP über SSL/TLS) nutzt SFTP ausschließlich SSH zur Absicherung und Steuerung. So funktioniert’s im Detail:

## 1. Aufbau der Verbindung
1. **[[SSH]]-Verbindung**
    - Client baut zunächst eine gewöhnliche SSH-TCP-Verbindung (Port 22) zum Server auf.
    - Darin wird per Diffie-Hellman/[[ECDH]] ein symmetrischer Session-Key ausgehandelt; alle folgenden Pakete sind verschlüsselt und mit HMAC gesichert.

2. **Subsystem-Request**    
    - Nach dem SSH-Handshake sendet der Client eine SSH-Message `SSH_MSG_CHANNEL_REQUEST` mit Typ `subsystem` und Name `"sftp"`.
    - Der Server öffnet daraufhin intern einen SFTP-Serverprozess (oder -Thread) und bestätigt.

## 2. Protokoll-Version & Erweiterungen
- **Version 3** ist der de facto-Standard, spezifiziert in **RFC 4253/4254/4255/4256**.
- Spätere Versionen (4–6) fügen Features wie Check-Functions, Directory-Attributes oder OpenSSH-Extensions hinzu.
- Client und Server verhandeln die höchste gemeinsame Protokoll-Version in ihrem ersten Paket.


## 3. Nachrichten- und Paketstruktur
1. **Pakete**
    - Jedes SFTP-Paket hat:
        1. **Packet Length** (uint32)
        2. **Type** (byte, z. B. 3=Request, 4=Data, 101=Open, 102=Close, …)
        3. **Request ID** (uint32)
        4. **Payload** (Typ-abhängige Felder)

2. **Typische Nachrichten­abläufe**    
    - **SSH_FXP_INIT (Client → Server)**: Gibt die gewünschte SFTP-Version an.
    - **SSH_FXP_VERSION (Server → Client)**: Bestätigt die Version und listet optionale Erweiterungen.
    - **SSH_FXP_OPEN**: Öffne eine Datei oder ein Verzeichnis (`filename`, Flags wie READ, WRITE).
    - **SSH_FXP_READ / WRITE**: Lese oder schreibe Datenblöcke (`offset`, `length`, `data`).
    - **SSH_FXP_CLOSE**: Schließe Handle.
    - **SSH_FXP_OPENDIR / READDIR / REMOVE / MKDIR / RMDIR / STAT / LSTAT**: Verzeichnis- und Dateiattribute-Operationen.
    - **SSH_FXP_STATUS**: Antworten auf alle Requests mit einem Statuscode (OK, EOF, FAILURE, PERMISSION_DENIED, …).

## 4. Handles & Sessions
- **Handles**: Wenn eine Datei oder ein Verzeichnis geöffnet wird, vergibt der Server ein **Handle** (opaque byte-String), das der Client für folgende Lese/Schreibe/Stat-Aufrufe verwenden muss.
- **Parallele Operationen**: Mehrere Handles gleichzeitig möglich, so kann man z. B. Dateien parallel lesen.


## 5. Fehler- und Status‐Management
- Jeder Request wird asynchron beantwortet: Client kann mehrere Requests senden, ohne vorherige Antworten abzuwarten.
- Statusmeldungen (`SSH_FXP_STATUS`) enthalten:
    - **Status code** (uint32, z. B. 0=OK, 1=EOF, 2=NO_SUCH_FILE…)
    - **Error message** (string)
    - **Language tag** (z. B. `"en"`)


## 6. Sicherheit und Authentifizierung
- **Gleicher Mechanismus wie SSH**: alle Auth-Methoden des SSH-Subsystems gelten (Public-Key, Passwort, Keyboard-Interactive).
- **Keine separate Authentifizierung** für SFTP nötig – erfolgt automatisch über den bestehenden SSH-User.
- **Ende-zu-Ende-Verschlüsselung** und **Integritäts­schutz** durch den SSH-Tunnel.

## 7. Vorteile von SFTP
- **Firewall-freundlich**: Nur ein Port (22) muss offen sein.
- **Einheitliches Security-Modell**: Keine separaten [[TLS]]-Konfigurationen wie bei FTPS.
- **Einfaches Auth-Management**: SSH-Keys, Agent-Forwarding, Kerberos/GSSAPI.
- **Feature-reich**: Verzeichniserstellung, Perms, Symlinks, Batch-Operationen, Resume-Support.


> **Zusammenfassung:**  
> _SFTP_ ist im Wesentlichen das **Datei-Subsystem von SSH**: Nach dem Aufbau einer verschlüsselten, authentisierten SSH-Verbindung wird über ein speziell verhandeltes Subsystem (Typ „sftp“) ein **eigenes Nachrichtenschema** etabliert, mit dem Dateien und Verzeichnisse sicher und effizient zu öffnen, lesen, schreiben und verwalten sind.