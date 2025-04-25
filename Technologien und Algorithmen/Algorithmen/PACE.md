The Password-Authenticated Connection Establishment (PACE) with negotiation of session keys is an authentication algorithm that is often used in electronic passports (EMRTDs), national eID cards and similar chips that follow ICAO Doc 9303 and BSI TR-03110.

## Why PACE?
- BAC's weaknesses. First-generation ePassports used Basic Access Control, where the chip derives 3DES session keys directly from the MRZ. 3DES-56 is weak, the keys are static, and an attacker can mount offline dictionary search of the machine readable zone (MRZ).
- PACE's goals. PACE raises the symmetric strength to AES/3DES-168, which eliminates offline guessing, and provides an authenticated Deffie-Hellman channel that freshens session keys on every inspection. It can be chained with Chip Authentication and Terminal Authentication to satisfy the full Extended Access Control (EAC) profile.

## How the chip and terminal negotiate an algorithm-suite ("session-key negotiation")
1. PACEInfo discovery
	- EF.CardAccess on the chip contains one or more PACEInfo structures. Each lists an Object Identifier (OID) that encodes:
		- mapping type (GM, IM or CAM)
		- key-agreement primitive (DH or ECDH)
		- symmetric cipher & MAC (3DES-CBC/CBC or AES-CBC/CMAC)
		- symmetric key length (128, 192, 256)
2. Suite selection
	- The terminal parses all advertised OIDs and picks the "best" one it implements (usually the strongest AES-256 variant)
	- It sends `MSE:Set AT` (IOS 7816-4) with that OID; the chip confirms or fails.
3. From here on both sides know the exact DH/ECDH group, block-cipher and MAC, so the key material derived later can be deterministically split into `KENC` (encryption) and `KMAC` (integrity) keys for secure messaging.

## Cryptographic Ingredients
| Component            | Purpose                             | Typical choices                                                     |
| -------------------- | ----------------------------------- | ------------------------------------------------------------------- |
| **Password `PWD`**   | Low‑entropy secret: MRZ, CAN, PIN   | MRZ (read optically), 6‑digit card-access number (CAN), or user PIN |
| **Key derivation**   | `K_PACE = SHA‑1(PWD                 |                                                                     |
| **Mapping function** | Turns `PWD` into a group element    | GM, IM or **CAM** (see §4)                                          |
| **Authenticated DH** | Establishes high‑entropy secret `Z` | DH MODP‑2048 or ECDH BP256 / P‑256                                  |
| **KDF**              | `K = SHA‑256(Z                      |                                                                     |
| **Secure messaging** | Protects further APDUs              | AES‑CBC with CMAC, or 3DES‑CBC/CBC                                  |
## Three Mapping Variants
| Variant                               | How the generator `ĝ` is built                                                                                                      | Performance / use‑case                                                   |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| **GM (Generic Mapping)**              | `ĝ = g·H(Nc ⊕ K_PACE)` in DH group                                                                                                  | Original mapping; easy to implement                                      |
| **IM (Integrated Mapping)**           | Maps `H(Nc ⊕ K_PACE)` _directly_ to a curve point; no extra DH multiplication                                                       | Fewer exponentiations on some curves                                     |
| **CAM (Chip‑Authentication Mapping)** | Extends GM by embedding _Chip Authentication_ inside PACE; chip signs its DH share with its CA key → active authentication for free | Standard in EU eIDs since ~2014, mandatory for German ID card since 2021 |

## Step-by-Step Protocol Flow (GM/ECDH Example)
|#|Command / Party|Detail|
|---|---|---|
|**0**|Chip → T|`GET CHALLENGE` → random nonce **Nc**|
|**1**|T|Computes `K_PACE` from MRZ / CAN • derives _transient_ curve generator `ĝ` using Nc|
|**2 a**|T → Chip|`GENERAL AUTHENTICATE` (phase 1): sends `P_T = ĝ·x_T`|
|**2 b**|Chip|Chooses random `x_C`, computes `P_C = ĝ·x_C`|
|**3**|Chip → T|`GENERAL AUTHENTICATE` (phase 2): returns `P_C`|
|**4**|Both|Compute shared secret `Z = P_T^{x_C} = P_C^{x_T}`|
|**5**|Both|`K = KDF(Z, context)` → split into `KENC`,`KMAC`; derive MACs `S_C`, `S_T`|
|**6 a**|T → Chip|`GENERAL AUTHENTICATE` (phase 3): sends `S_T`|
|**6 b**|Chip → T|`GENERAL AUTHENTICATE` (phase 4): replies `S_C`|
|**7**|Both|Verify peer’s MAC → _mutual authentication complete_; secure messaging with `KENC`,`KMAC` starts|
Internally the sequence counter SSC = `Nonce_T || Nonce_C` (incremented per APDU) feeds the CMAC, giving forward secrecy and replay protection at the APDU layer.

## Security Properties (Informal)
- No offline dictionary attack. An attacker must interact with the chip for every password guess; rate-limiting and tamper sensors on the chip restrict brute force
- Mutual authentication & forward secrecy. The MACs cover both DH shares and all preceding messages; the DH secret is ephemeral
- Chiper-suite agility. OIS-based negotiation allows future migration to larger curves or post-quantum KEMs without changing higher-level EAC logic.
- Composable with CA/TA. CAM reuses the PACE DH transcript to verify the chip's static CA key, shortening the setup from ~$1$s to a few hundred ms on typical NFC hardware.


## Extensions & Implementation notes
- PIN-protected PACE. For eID cards the password may be a user-entered PIN. Wrong attempts decrement a retry counter; after three failures the chip locks.
- "PACE v2" / post-quantum. Recent drafts add Curve448/Brainpool512 and negotiate SHA-384/512 as KDF; NIS PQC candidates are being prototyped for future SAC revisions.
- Hardware acceleration. Some chips cache the mapped generator across session, halving the start-up time when the same password is reused (e.g. CAN based reading)
- RFC 6631. The same PACE idea is adapted to IKEv2 for network VPNs, showcasing PACE's generality beyond smardcards.
