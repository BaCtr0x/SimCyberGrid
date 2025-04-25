## General
First ECKA stands for `Elliptic-Curve Key Agreement`, which is the shorthand that is used by the BSI, on most cases it is shortened to `EC`. Second, DH stands for `Diffie-Hellman`, which is a classic two-party key-agreement or key-exchange scheme.
So ECKA-DH is the elliptic-curve analogue to DH: two parties combine their private key with the other party's public key to obtain a shares secret. In the Smart-Meter-Gateway world the operation is performed inside the certified [[Security Module]] and then handed to the [[Gateway]] firmware for the KDF and later use. 

## Mathematical Core (Single-pass "basic" ECKA-DH)
| Party     | Static data                                                                   | Ephemeral (optional)                      |
| --------- | ----------------------------------------------------------------------------- | ----------------------------------------- |
| **Alice** | Private key _d<sub>A</sub>_  <br>Public key _Q<sub>A</sub> = d<sub>A</sub>·G_ | Optional _dʹ<sub>A</sub>, Qʹ<sub>A</sub>_ |
| **Bob**   | Private key _d<sub>B</sub>_  <br>Public key _Q<sub>B</sub> = d<sub>B</sub>·G_ | Optional _dʹ<sub>B</sub>, Qʹ<sub>B</sub>_ |
1. **Key Agreement**
   _Alice computes_ _S = d<sub>A</sub> · Q<sub>B</sub>_  
   _Bob computes_  _S = d<sub>B</sub> · Q<sub>A</sub>_
   Both multiplications produce the **same point** _S (x, y)_ because elliptic‑curve multiplication is commutative in that form.
2. **Extract the "shared secret"**
   The _x_‑coordinate (or a hash thereof) is fed into a key‑derivation function (KDF). In the PP this KDF is X9.63/HKDF, yielding the traffic‑keys for TLS or the “key‑encryption‑key” for CMS.
3. **Result**
   No private key ever leaves its owner; eavesdroppers who see _Q<sub>A</sub>_ and _Q<sub>B</sub>_ cannot derive _S_ unless they can solve the Elliptic Curve Discrete Logarithm Problem.

## Protocol Flavours
|Flavour|What changes|Typical use in SMGW|
|---|---|---|
|**Static‑Static**|Each side uses its long‑term key pair once per installation.|Content‑data encryption to market participants.|
|**Ephemeral‑Static (ECDHE)**|The client (and sometimes the server) generates a fresh key pair per session.|TLS 1.2/1.3 hand‑shake (forward secrecy).|
|**Cofactor diffie‑hellman**|Scalar multiplied by the curve’s co‑factor _h_ to defeat small‑sub‑group attacks.|Required by BSI TR‑03111 for many curves.|

## Step-by-Step inside a TLS 1.2 Handshake (ECDHE with certificate)
1. **Hello / ServerHello** - server advertises an ECDHE-capable cipher-suite
2. **Key-exchange messages**
	- Client sends _Qʹ<sub>C</sub>_
	- Server replies with _Qʹ<sub>S</sub>_ **signed** by its static ECDSA key to authenticate itself.
3. **Both sides run ECKA-DH** with (dʹ<sub>C</sub>, Qʹ<sub>S</sub>) or (dʹ<sub>S</sub>, Qʹ<sub>C</sub>).
4. **PRF / HKDF** derives the Master Secret and finally the symmetric traffic keys (AES-GCM/HMAC)
5. **Forward secrecy** stems from the fact that dʹ<sub>∗</sub> dies after the session.

## Security Parameters & Curve Choice
|Parameter|Typical value (BSI)|Why|
|---|---|---|
|Curve|Brainpool P256r1 / P384r1|Listed in BSI‑TR‑03111; designed in Germany.|
|Key length _d_|256 / 384 bits|≈128 / 192‑bit symmetric strength.|
|KDF|X9.63 w/ SHA‑256 or SHA‑384|Matches the curve strength; required in PP.|
|Cofactor|h = 1 or 2|Small → small‑sub‑group attacks easy to defeat.|
## implementation & Operational Hints
- **Key validation** - Always check that a received public key lies on the curve and is not the point at infinity.
- **Side-channel resistance** - Multiply with constant-time algorithms (Montgomery ladder, windowed NAF with blinding) and insert random delays in the security-module.
- **Random-number quality** - Ephemeral keys MUST come from a deterministic random bit generator (DRBG) with at least $128$-bit security; see TR-03111, section RNG requirement.
- **Key-lifetime** - For static keys follow the PP's life-cycle rules; ephemeral keys are destroyed right after the TLF-Finish.
- **Certificate binding** - When ECKA-DH is used with static keys (e.g. CMS), the corresponding public-key certificate must be stored in - and verified by - the security-module

## How ECKA-DH differs from ECKA-EG
|Aspect|**ECKA‑DH**|**ECKA‑EG**|
|---|---|---|
|Purpose|Derive a **shared secret**|Encrypt a **payload key** for the partner|
|“Round‑trips”|Symmetric: both compute S once|Asymmetric: encrypt → decrypt|
|Used in PP|TLS key agreement, CMS KEK derivation|Content‑data encryption when the sender cannot perform DH (rare in SMGW)|

## Numeric Mini-Example (secp256r1)
1. Curve generator _G_ (short form): _(x = 6b17d1…, y = 4fe342…)_
2. Alice picks _d<sub>A</sub>= 0x1C97 …_ and sends _Q<sub>A</sub> = d<sub>A</sub>·G_.
3. Bob picks _d<sub>B</sub>= 0x233B …_ and sends _Q<sub>B</sub> = d<sub>B</sub>·G_.
4. Alice computes _S = d<sub>A</sub>·Q<sub>B</sub> = (04A96C …, 23CE91 …)_.
5. Bob obtains the exact same point.
6. Feed _S.x_ into X9.63‑KDF → session key 0x5A 41 … 71.

## Why use ECKA-DH
- Enables forward secrecy for every remote session, even if the device lives in the field for 15 years.
- Fits into constrained hardware: a complete scalar-multiplication on Brainpool P256 $\approx1$ ms on modern security controller
- Interoperates with market PKI and CMS wrapping, which the gateway has to support