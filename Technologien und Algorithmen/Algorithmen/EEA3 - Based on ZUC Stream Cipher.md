## Overview
- EEA3 is based on the ZUC stream cipher (Zu Chongzhi), selected for LTE and 5G, particularly for compatibility with Chinese national standards
- A strong, lightweight stream cipher, optimized for hardware and software

## Structure
- **Key size:** $128$ bits
- **IV:** $128$ bits, including:
	- COUNT ($32$ bits)
	- BEARER ($5$ bits)
	- DIRECTION ($1$ bit)
	- Zero padding

## Internals:
- ZUC uses:
	- A non-linear feedback shift register (NLFSR) of $16 \ 31$-bit registers
	- A bit reorganization layer
	- A non-linear finite state machine (FSM) for keystream generation

## How it Works
1. Initialize ZUC with key and IV
2. Discard the first $32$ bits (warm-up phase)
3. Generate $32$-bit keystream words
4. Encrypt plaintext with XOR

## Security
- ZUC is cryptographically strong and has passed extensive analysis in Europe and China
- Still used in 5G (5G-NR) as NEA3/NIA3