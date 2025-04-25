## General
**Brainpool** is a _family_ of prime‑field elliptic‑curve domain parameters published by the German Federal Office for Information Security (BSI). They are standardized in **RFC 5639** and BSI **TR‑03111** and are named _brainpoolP160r1, …, brainpoolP512t1_ (P = prime‑field, r = random curve, t = “twisted” co‑factor‑1 variant). Typical uses: [[ECDSA]], ECDH / [[ECKA-DH]], and [[TLS]] in German e‑ID cards, [[Gateway|Smart-Meter Gateway]], ePassport chips, automotive V2X, etc.


## Why They were Created
|Goal|How Brainpool addresses it|
|---|---|
|**Transparency** – avoid the “NSA back‑door” debate around NIST curves.|Parameters generated from _public_ pseudo‑random seeds + completely documented generation algorithm.|
|**Modern security levels**|Curves sized for 80 → 256 bit symmetric strength (160–512‑bit curves).|
|**Rigorous safety checks**|Each candidate curve is accepted only if it passes 11 criteria: large prime order, cofactor = 1, MOV‑resistance, CM discriminant, twist security, etc.|

## How a Brainpool Curve is Generated
1. **Choose a bit‑length** _m_ (160, 192, 224, … , 512).
2. **Generate a provably random prime _p_**
```go
  seed  := SHA‑1("Brainpool"+m) p     := next_prime( 2^(m‑1) + int(seed) mod 2^(m‑1) )
```    
Iterate until $p \equiv 3 (\mod 4)$ and passes primality test.
3. **Define curve coefficients**
```go
A := int( SHA‑1(seed || "A") ) mod p B := int( SHA‑1(seed || "B") ) mod p
```
Repeat with seed ++ while $(4\cdot A^3 + 27 \cdot B^2) \equiv 0 (\mod p)$.
4. **Compute curve order** $n = \#E(\mathbb{F}_p)$ with Schoof–Elkies–Atkin.  
    Accept only if _n_ is prime and $h = \lceil \#E / n \rceil = 1$.
5. **Derive base point G**
    ```go
   xG := int( SHA‑1(seed || "Gx") ) mod p yG := sqrt( xG^3 + A xG + B mod p ) 
```
    Choose the positive root that makes _G_ of order _n_.
    

Because every step is deterministic from the public seed, **anyone can reproduce the parameters** and be sure no hidden structure was inserted.

## Using a Brainpool Curve in Practice
1. **Key generation**
	pick random  $1 \leq d < n$
	$Q = d \cdot G$               // scalar‑multiplication
	RFC 5639 requires an approved DRBG and cofactor multiplication ($h = 1$ so no adjustment needed).

2. **ECKA‑DH / ECDH**
	Shared $secret = d_A \cdot Q_B = d_B \cdot Q_A (point S)$.
	Feed S.x into X9.63 / HKDF to derive AES or HMAC keys (see TR‑03111).

3. **ECDSA signatures**
	Same formulas as NIST curves; just plug in the Brainpool domain parameters.

## Security & Performance Notes
- **No known backdoors** - parameters look indistinguishable from random and the seed is published
- **Twist security** - cofactors of the curve and its quadratic twist are $1$, blocking small-sub-group attacks
- **Performance** - $\approx 5-15\%$ slower than NIST P-256 because $a \neq -3$, removing a common multiplication shortcut
- **Side-channels** - use constant-time ladder or windowed NAF + random scalar blinding; see BSI TR-03111 chap 3.

## Brainpool vs NIST/SEC Curves
| Aspect           | Brainpool                             | NIST P‑curves                                           |
| ---------------- | ------------------------------------- | ------------------------------------------------------- |
| Parameter origin | Deterministic seed → verifiable       | “Random seed” – opaque                                  |
| Cofactor         | 1                                     | 1                                                       |
| Twist security   | enforced                              | not guaranteed (P‑256 twist has _h = 1_, others larger) |
| Adoption         | European e‑ID, German SGW, automotive | Almost all global PKI, TLS default                      |
| Speed            | Slightly slower (a ≠ −3)              | Very fast (a = −3)                                      |