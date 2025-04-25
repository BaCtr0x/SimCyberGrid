## Definition
A stream cipher is a type of symmetric-key encryption algorithm that encrypts plaintext one bit or byte at at time. It generates a keystream ( a sequence of pseudo-random bits), which is then XORed with the plaintext to produce the ciphertext.
```Pseudocode
Ciphertext (C) = Plaintext (P) ⊕ Keystream (K)
Plaintext (P)  = Ciphertext (C) ⊕ Keystream (K)
```
It is called a stream cipher because the encryption/decryption happens as a continuous stream, bit-by-bit or byte-by-byte.

## Components
### 1. Key (K):
- A secret shared between sender and receiver. Typically 64, 128,256 bits.
### 2. Initialization Vector (IV):
- A non-secret random or pseudo-random number used to ensure taht repeated encryption of the same message with the same key yields different ciphertexts
### 3. Key Scheduling Algorithm (KSA):
- Initializes the internal state (e.g., registers or memory) based on the key and IV.
### 4. Pseudo-Random Generation Algorithm (PRGA):
- Continuously generates keystream bits/bytes from the internal state.
### 5. XOR Operation
- Keystream is XORed with plaintext to produce ciphertext.

## Modes of Operation
### Synchronous Stream Cipher:
The keystream is generated independently of the plaintext and ciphertext (e.g. RC4). Synchronisation is crucial.

### Self-Synchronous (Asynchronous) Stream Cipher:
The keystream depends on previous ciphertext bits (e.g., Cipher Feedback Mode - CFB). It can recover synchronization automatically after bits errors.

## Internal Mechanisms
### 1. Linear Feedback Shift Registers (LFSRs):
- Widely used in lightweight stream ciphers (e.g., GEA, A5/1).
- An LFSR consists of a shift register whose input bit is a linear function (XOR) of its previous state.
- Each clock cycle shifts the bits and feeds back a new input.
```Math
s(t) = a₁·s(t-1) ⊕ a₂·s(t-2) ⊕ ... ⊕ aₙ·s(t-n)
```

### 2. Non-Linear Filters and Combining Functions:
- Output of LFSRs is fed into a non-linear Boolean function to produce pseudo-random keystream bits.
- This prevents linear cryptanalysis and improves security.

## Security Goals $ Threats
### Desirable Properties:
- **Long Period:** Keystream should not repeat (ideally $2^n$ for an $n$-bit internal state)
- **Randomness:** Keystream should pass statistical randomness tests.
- **Resistance to Known Attacks:** Algebraic attacks, correlation attacks, distinguishing attacks

### Common Attacks:
- **Known-plaintext attacks (KPA):** Exploit predictability in the keystream.
- **Key recovery attacks:** Recover internal state or secret key.
- **Algebraic attacks:** Solve equations relating keystream bits to internal state.
- **Time-Memory Trade-Off (TMTO):** Precompute keystream-state pairs (e.g. rainbow tables)

## Modern Secure Stream Ciphers
|Cipher|Use Case|Notes|
|---|---|---|
|**ChaCha20**|TLS, VPNs (e.g., WireGuard)|Highly secure, fast, nonce-based|
|**Salsa20**|Cryptographic APIs|Predecessor to ChaCha|
|**Grain**|Lightweight applications|Uses LFSRs + non-linear filters|
|**Trivium**|Hardware-focused environments|Designed for simplicity & speed|