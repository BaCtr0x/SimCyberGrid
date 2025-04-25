GSM (Global System for Mobile Communications) is the second generation (2G) of cellular network technology, standardized by ETSI in the early 1990s. It introduced digital voice and basic data services (SMS, GPRS) and became the most adopted mobile standard globally.

## How GSM Works (High-Level Architecture)
### 1. Network Components
- **Mobile Station (MS)** - The user's phone wit ha SIM card (stores keys & identity)
- **Base Transceiver Station (BTS)** - Handles radio communication
- **Base Station Controller (BSC)** - Manages multiple BTS
- **Mobile Switching Center (MSC)** - Handles all routing, authentication
- **HLR/VLR** - Home/Visitor Location Registers for subscriber info

### 2. Authentication & Key Derivation
GSM uses a challenge-response authentication mechanism:
1. Network sends a random challenge (RAND) to the SIM
2. SIM uses its secret key `K` and `RAND` to compute a response:
```Keys
SRES = A3(K, RAND)
Kc = A8(K, RAND)  # Session Key
```
3. The network performs the same computation and checks `SRES`
4. The session key `Kc` is then used to encrypt communications.

### 3. Encryption
GSM uses symmetric stream ciphers for over-the-air encryption:
- A5/1, A5/2, A5/3 for voice & SMS
- GEA-1, GEA-2, GEA-3 for GPRS data
The encryption starts once authentication succeeds. Encryption happens at the air interface, meaning between the phone and BTS, but not end-to-end.

## Security of GSM: Classical & Quantum Context
### Classical Issues:
- **A5/1:** Broken with rainbow tables or real-time decryption
- **A5/2:** Extremely weak - deprecated
- **A5/3:** Based on KASUMI - better, but structurally flawed (see [[UEA1 - Based on KASUMI]])
- **GEA-1/2:** Known to be breakable; GEA-1 had a backdoor and GEA-2 kinda, see [[GAE-1 and GAE-2 Cryptanalytic Attacks Overview]]

### Quantum View:
- GSM relies entirely on symmetric crypto, so:
	- Grover's algorithm weakens A5/3 and GEA-3, but they survive if key length is sufficient
	- However, key lengths are mostly only $64$ bits (A5/1, GEA-1) $\rightarrow$ unsafe even without quantum

## Structural Limitations
- No mutual authentication in GSM: the network does not prove its identity $\rightarrow$ Enables IMSI catchers, fake BTS (stingrays), and downgrade attacks
- No integrity protection $\rightarrow$ The network can modify data or inject message, and the phone can't verify

## GSM in Context of [[UMTS 3G]], [[LTE 4G]] and Quantum Security
|Technology|Key Crypto|Authentication|Integrity|Quantum-Safe?|Deployment Status|
|---|---|---|---|---|---|
|**GSM (2G)**|A5, GEA|One-way (SIM only)|❌ None|❌ No (64-bit keys)|Legacy / being retired|
|**3G (UMTS)**|KASUMI, SNOW 3G|✅ Mutual|✅ Yes|⚠️ Partial (128-bit)|Still active in some regions|
|**LTE (4G)**|AES, SNOW 3G, ZUC|✅ Strong mutual|✅ Yes|⚠️ Partial|Widely deployed|
|**5G**|AES, ZUC, PQC (planned)|✅ With SUCI|✅ Strong|✅ Ready with PQC|Growing deployment|
