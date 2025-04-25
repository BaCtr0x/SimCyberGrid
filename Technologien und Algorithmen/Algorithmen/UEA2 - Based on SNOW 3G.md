## Overview 
- UEA2 (UMTS Encryption Algorithm 2) is based on the SNOW 3G stream cipher.
- Chosen to strengthen the encryption scheme and address cryptanalytic weaknesses in [[UEA1 - Based on KASUMI|UEA1]].

## Structure
- [[Stream Cipher]], not a block cipher
- Key size: $128$ bits
- IV size: $128$ bits constructed from:
	- COUNT ($32$ bits): frame-dependent counter
	- BAERER ($5$ bits): logical channel ID
	- DIRECTION ($1$ bit): uplink/downlink flag
	- Padding: zeroes to reach $128$ bits

## Components
### 1. Linear Feedback Shift Register (LFSR)
- $16$ registers of $32$ bits
- Operates over $GF(2^{32})$, designed for good diffusion and large period
### 2. Finite State Machine (FSM)
- Uses internal registers (R1, R2)
- Computes non-linear transformation using modular addition, XOR, and bitwise operations

### 3. Keystream Generation
- LFSR initialized with key and IV
- FSM combines LFSR output with non-linear operations to produce a $32$-bit keystream word per cycle
- Keystream is XORed with plaintext to encrypt

## How it Works
- Similar to other stream ciphers:
``` XOR
C = P ⊕ Z
```
	Where:
	- `C` = ciphertext
	- `P`= plaintext
	- `Z`= keystream from SNOW 3G
- Used in both encryption (UEA2) and integrity protection (UIA2)

## Security
- SNOW 3G is considered secure and is still used in LTE (EEA1)
- It has good resistance against differential and algebraic attacks