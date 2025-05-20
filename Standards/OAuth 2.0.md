## Zweck & Anwendungsgebiet
- **Autorisierung** dezentraler Anwendungen: Ermöglicht Clients (Web-Apps, Mobile Apps, Microservices), im Namen eines Nutzers oder im eigenen Kontext sicher auf Ressourcen-APIs zuzugreifen, ohne Passwörter weiterzugeben.
- Weit verbreitet in **REST-APIs**, Single-Page-Applications, Mobile- und IoT-Szenarien.

## Architektur & Message-Flows

- **Rollen**
    1. **Resource Owner** (Nutzer oder System, das Zugriff besitzt)
    2. **Client** (Anwendung, die Zugriff anfordert)
    3. **Authorization Server** (vergibt Tokens nach erfolgreicher Authentisierung/Autorisierung)
    4. **Resource Server** (API, die durch OAuth-Tokens geschützt ist)

- **Typische Flows (Grant-Types)**    
    1. **Authorization Code**
        - Browser-Redirect: Client leitet User zum Auth-Server, holt Code, tauscht Code gegen Access-Token.

    2. **Client Credentials**        
        - Maschine-zu-Maschine: Client tauscht Client-ID/Secret direkt gegen Token.

    3. **Implicit** (für Public Clients / SPAs, heute weniger empfohlen)        
        - Access-Token direkt als Fragment im Redirect.

    4. **Resource Owner Password Credentials** (ROP-C)        
        - Client übergibt Nutzername/Passwort an Auth-Server und erhält Token (nur in vertrauens­würdigen Apps).

- **Token-Laufzeit & Refresh**    
    - **Access Token** (kurze Gültigkeit, z. B. 5–60 Minuten)
    - **Refresh Token** (längere Gültigkeit, z. B. Tage–Monate), um neue Access Tokens ohne erneute User-Interaktion zu holen


## Datenmodelle & Token
- **Access Token**
    - Kurzlebiges Bearer-Token (Opaque String oder JSON Web Token – JWT)
    - Trägt Claims wie `sub`, `scope`, `exp`, `aud`, `iss`
- **Refresh Token**
    - Opaque oder JWT, nur an vertrauenswürdige Clients ausgegeben
- **ID Token** (bei OpenID Connect)
    - JWT mit Nutzer-Identität (`sub`, `email`, `name`)
- **Parameter & Endpoints**
    - `/authorize` (GET) für User-Consent und Code-Generierung
    - `/token` (POST) für Token-Austausch (Code → Token, Client Credentials)
    - `/introspect` (RFC 7662) zur Token-Validierung
    - `/revoke` (RFC 7009) zum Widerruf von Tokens


## Security
- **[[TLS]]** zwingend für alle Endpoints
- **Proof Key for Code Exchange (PKCE)** bei Public Clients (SPAs/Mobile)
- **Client Authentication**
    - Confidential Clients via Client-ID/Secret (Basic Auth oder Form-POST)
- **Scopes** granular für Ressourcenzugriff
- **Token Binding** / **Mutual TLS** (mTLS) für erhöhte Sicherheit gegen Token-Diebstahl

## Typische Use-Cases
1. **Single-Page-Applications**: Browser-App erhält Access-Token via Authorization Code + PKCE
2. **Mobile Apps**: native App nutzt PKCE-Flow für User-Login
3. **Microservices**: Service A ruft Service B mit Client-Credentials-Token auf
4. **IoT Devices**: eingeschränkte Clients holen sich Device-Tokens via ABAC- oder PSK-basiertem Flow
5. **Externe Partner-APIs**: Drittanbieter greifen via OAuth-Token auf geschützte Ressourcen zu

> **Kurz:**  
> _OAuth 2.0 trennt Authentisierung (wer bist du?) vom Autorisierungs­token (was darfst du?). Es nutzt standardisierte Endpoints und Token-Typen, um Clients kontrolliert und sicher Zugriff auf Ressourcen zu gewähren._