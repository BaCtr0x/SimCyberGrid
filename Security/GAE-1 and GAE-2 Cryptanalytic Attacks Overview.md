## Background
- [[GEA-x Family#GEA-1 - Proprietary, Backdoored|GEA-1]] and [[GEA-x Family#GEA-2 - Obfuscated, Not Backdoored|GEA-2]] are proprietary [[Stream Cipher|steam ciphers]] used for encryption [[GSM - Second Generation (2G)]] (2G mobile data)
- Both algorithms use a $64$-bit session key and generate $1600$ bytes of keystream per session.
- GEA-1 was designed under export control restrictions, likely limiting its strength intentionally.

## GAE-1 Attack
### Key Observation
- GAE-1 uses three LFSRs (31, 32, 33 bits) and a nonlinear Boolean function $f$.
- The initialization is done through a non-linear feedback register S, which feeds into the three LFSRs.
- **Critical Weakness:** The joint initial state of registers A and C only spans $2^{40}$ states, not the expected $2^{64}$ - a serious entropy loss likely introduced by design.

### Attack Method (Divide-and-Conquer)
1. Precomputation:
	- Build a lookup table (Tab) from $2^{32}$ values of possible states for Register B.
	- Requires $\approx 44.5$ GiB and $2^{37}$ GEA-1 evaluations
2. Online Attack:
	- Given $65$ bits of known keystream ($24$ bits from one frame), perform a meet-in-the-middle attack on the states of A and C.
	- Match against Tab to recover the full internal state.
3. Key Recovery:
	- Once the initial state is known, recover the key by reversing the initialization process.

### Complexity
- **Time:** ~$2^{40}$ GEA-1 evaluations per session key
- **Memory:** $44.5$ GiB
- Data: $65$ bits of known keystream (can come from predictable protocol headers)

## GEA-2 Attack
### Key Observation
- GEA-2 adds a fourth LFSR ($29$ bits) and improves initialization
- No obvious structural weaknesses like in GEA-1
- However, the stream generation remains algebraically weak and susceptible to algebraic and list merging attacks

### Attack Method
1. Keystream Requirements:
	- Requires all $1600$ bytes ($12\ 800$ bits) of keystream.
	- This can be obtained through predictable plaintext (e.g. attacker-controlled traffic)
2. Hybrid Attack:
	- Combines:
		- **Algebraic cryptanalysis** (using linearization of the boolean filtering function)
		- **Guess-and-determine** (guess bits of internal state to reduce complexity)
		- **List merging / Meet-in-the-Middle** (recover register states B and C)
3. Optimizations:
	- Preprocessing with Gaussian elimination and bit slicing
	- Use of partial keystreams (e.g. sliding window masks)

### Complexity
- **Time:** ~$2^{45.1}$ GEA-2 evaluations
- **Memory:** ~$32$ GiB (hash table for B/C state collision)
- **Data:** Requires $1\ 600$ bytes of known keystream

## Summary Table
| Algorithm | Type          | Key Size  | Effective Security           | Attack Method                     | Complexity              | Data Required             |
| --------- | ------------- | --------- | ---------------------------- | --------------------------------- | ----------------------- | ------------------------- |
| GEA-1     | Stream cipher | $64$ bits | ~$40$ bits (due to backdoor) | Divide-and-Conquer + Table lookup | ~$2^{40}$ GEA-1 evals   | $65$ keystream bits       |
| GEA-2     | Stream cipher | $64$ bits | ~$45$ bits (no backdoor)     | Algebraic + List merging          | ~$2^{45.1}$ GEA-2 evals | $1 \ 600$ keystream bytes |
