A5/x is a family of [[Stream Cipher]] that encrypt over-the-air voice traffic in circuit-switched [[GSM - Second Generation (2G)]]

## A5/1 - Designed for Europe (1990s)
- **Type:** Stream Cipher
- **Key size:** $64$ bits (from `Kc` session key)
- **Structure:**
	- Uses three LFSRs ($19$, $22$ and $23$ bits)
	- Controlled by majority clocking - irregular update depending on clock bits
- **keystream Generation:**
	- Initialize LFSRs with `Kc` and frame number
	- Output is XORed with plaintext bits (voice)

### Security
- Reverse-engineered and publicly broken in 2000s
- Time-Memory Trade-Off and SAT-based attacks can recover `Kc` in seconds to minutes
- Tools like Kraken and RainbowCrack automate attacks

## A5/2 - Weakened Export Version
- Deliberately weakened for export controls
- Only $2.5$ KB RAM required to break
- Uses $4$ LFSRs, but with linear dependencies that enable real-time attacks
- Completely insecure - deprecated and banned

## A5/3 - Stronger Cipher (KASUMI)
- Blocker cipher-based, not a traditional stream cipher
- Based on KASUMI, a lightweight version of MISTY1
- Operates in counter mode (CTR) - simulates a stream cipher

### Security
- Much stronger than A5/1/2, but still has related-key attacks
- Can withstand passive attacks, but vulnerable if KASUMI key scheduling is misused
