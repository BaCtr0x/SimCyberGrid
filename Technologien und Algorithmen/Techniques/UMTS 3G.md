This is one of the communication standards that the SMART Grid architecture will be base on, so we note some important information here. UMTS stands for universal Mobile telecommunications system. It is used for Voice, SMS and high-speed data.

## Encryption
- [[UEA1 - Based on KASUMI]]
- [[UEA2 - Based on SNOW 3G]]


## Quantum Impact
- UEA1 (KASUMI): Already weak - does not need a quantum adversary to break
- UEA2 (SNOW 3G):
	- Grover's algorithm gives an effective $64$-bit security level (from $128$-bits)
	- Marginally acceptable but will require eventual replacement in high-assurance environments
$\rightarrow$
- Not quantum secure
- Already deprecated globally
- No path for quantum (algorithms hardcoded in legacy baseband processors)
- Networks are actively phasing out 3G; quantum transition is irrelevant for it long-term 
	- This does not apply to the smart grid as this technology is just introduced to the entire system, hopefully they will use mainly 4G