## Overview
- UEA1 (UMTS Encryption Algorithm 1) is a block cipher based on KASUMI, which is itself a modified version of MISTY1 (designed for hardware efficiency)
- UEA1 was used to encrypt both user and control plane traffic in 3G networks

## Structure
- KASUMI is an $8$-round Feistel network
- Block size: $64$ bits
- Key size: $128$ bits

## How it works
### Key Scheduling
- A $128$-bit input key is expanded into multiple round subkeys using rotation and non-linear functions

### Rounds
Each round of KASUMI includes:
- FL function: Non-linear Boolean and rotation-based operation
- FO function: Three-round Feistel-like network inside the main round
	- used FL function: Incorporates two fixed S-boxes (S7 and S9)

### Encryption Process (for UEA1)
- Takes $64$-bit input blocks (plaintext)
- Uses counter mode (CTR) to convert KASUMI into a stream cipher
- Each $64$-bit keystream block is XORed with plaintext to get ciphertext

![Block diagram of KASUMI encryption algorithm. The cipher consists of eight rounds shown in left. The structure of the non-linear functions used in each round is shown in the bottom and right. The round function uses a round key which consists of eight 16-bit subkeys derived from the original 128-bit cipher key using a fixed key schedule.](https://www.researchgate.net/profile/Massoud-Masoumi/publication/323178155/figure/fig1/AS:631586865303584@1527593451268/Block-diagram-of-KASUMI-encryption-algorithm-The-cipher-consists-of-eight-rounds-shown.png)

## Security
- KASUMI was initially considered secure but known-plaintext and related-key attacks have weakened its confidence
- Vulnerabilities arise when attackers can manipulate key material or exploit improper use.