This is the other communication standard that will be used for the communication of the Smart Grid architecture. It is an advanced version of the 3G protocol and depending on the implementation uses the same encryption or is based on AES or ZUC. LTE stands for long term evolution.

## Encryption
- [[EEA1 - Based on SNOW 3G]]
- [[EEA2 - Based on AES in CTR Mode]]
- [[EEA3 - Based on ZUC Stream Cipher]]

## LTE Encryption Algorithm Comparison
|Feature|**EEA1** (SNOW 3G)|**EEA2** (AES-CTR)|**EEA3** (ZUC)|
|---|---|---|---|
|Type|Stream cipher|Block cipher in CTR mode|Stream cipher|
|Key Size|128 bits|128 bits|128 bits|
|Keystream Output|32-bit words|128-bit blocks|32-bit words|
|Performance|Efficient|Very fast with AES-NI|Very fast in both HW/SW|
|Security Status|Strong|Strong, NIST-approved|Strong, used in 5G too|
|Standard Usage|Global|Global|Required in China, optional elsewhere|
## Summary
- EEA1: Reuses SNOW 3G - good legacy support and performance
- EEA2: Uses AES-CTR - highly secure, efficient, globally supported
- EEA3: Based on ZUC - strong and efficient, especially in China and 5G context


## Security in the Quantum Era
### Quantum Impact
- EEA1 (SNOW 3G)
	- $128$-bit key $\rightarrow$ reduced to ~$64$-bit effective security with Grover
	- still usable, but long-term risk
- EEA2 (AES-$128$ in CTR mode)
	- AES-$128$ drops to ~$64$-bit strength under Grover
	- AES-$256$ recommended in quantum-aware environments
	- CTR mode itself remains secure under quantum threats if the key is long enough.
- EEA3 (ZUC)
	- No known quantum breaks, but $128$-bit key also susceptible to Grover
	- Cryptanalysis shows no structural weakness today, but key length is borderline

### LTE Quantum Transition Readiness:
- Symmetric encryption is relatively safe - but key length must increase
- No port-quantum (PQC) public key primitives are used in LTE anyway ; keys are derived via symmetric mechanisms (e.g. from SIM card)
- Main exposure is during key exchange and authentication (e.g. AKA protocol)