## Overview
- Uses AES-$128$ in Counter (CTR) mode to convert the block cipher into a stream cipher
- Favored for its hardware acceleration (e.g. AES-NI) and NITS approval

## Structure
- **Key size:** $128$ bits
- **Block size:** $128$ bits
- IV construcion:
	- COUNT ($32$ bits)
	- BEARER ($5$ bits)
	- DIRECTION ($1$ bit)
	- Followed by $0$-padding to $128$ bits

## How it Works
### 1. CTR Block Generation
- An IV block is created and incremented to generate the counter blocks

### 2. Encryption
- Each counter block is encrypted with AES using the shared key
- The result is XORed with plaintext blocks to produce ciphertext.
```ini
C_i = P_i ⊕ AES_K(CTR_i)
```

## Security
- AES-CTR is provably secure under standard assumptions
- Fast and suitable for high-throughput LTE data links


