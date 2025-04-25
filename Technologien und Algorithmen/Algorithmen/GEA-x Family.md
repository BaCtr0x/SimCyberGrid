The GEA-x family is used to encrypt the packet-switched data in [[GSM - Second Generation (2G)]]

## GEA-1 - Proprietary, Backdoored
- **Key size:** $64$ bits
- **Structure:**
	- 3 LFSRs ($31$, $32$, $33$ bits)
	- Complex Boolean filtering function
- **Design flaw:** The joint state space is only $2^{40}$, not $2^{64} \rightarrow$ intentional entropy reduction

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

### Status
- Brocken and backdoored - suspected intentional weakening for lawful interception

## GEA-2 - Obfuscated, Not Backdoored
- **Key size:** $64$ bits (same as GEA-1)
- Improved initialization and non-linear feedback

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
$\rightarrow$ Still not secure by modern standards