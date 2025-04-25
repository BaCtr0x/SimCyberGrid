The target of evaluation (TOE) is an electronic unit comprising hardware and software used by the Gateway for central cryptographic services and secure storage of cryptographic keys and further data relevant to the Gateway. The TOE is intended to be used by the Gateway for its operation in a Smart Metering System as a cryptographic  service provider for different cryptographic functionalities based on elliptic curve cryptography as the generation and verification of digital signatures and key agreement which is used by the Gateway in the framework of TLS, content data signatures and content data encryption.

The following figure provides an overview over the TOE as part of a complete Smart Metering System from a purely functional perspective as used in this Protection Profile (PP). Note that the arrows indicate a bi-directional information flow, but not a bi-directional communication flow initialization.
![[TOE_Direct_Environment.png]]

### Components
- [[Gateway]]
- [[Meter]]
- [[Security Module]]
- [[Controllable Local Systems]]

### TOE in the Smart Metering System
The TOE is the security module of the smart metering system and thus support the Gateway specific cryptographic needs and thus is responsible for certain cryptographic services that are invoked by the Gateway for its operation in a Smart Metering System. These services are:
- Digital Signature Generation
- Digital Signature Verification
- Key Agreement for [[TLS]]
- Key Agreement for Content Data Encryption
- Key Pair Generation
- Random Number Generation
- Component Authentication via the [[PACE]] Protocol with Negotiation of Session Keys
- Secure Messaging
- Secure Storage of Key Material and further data relevant for the Gateway

### TOE Type
The Security Module (TOE) is a service provider for the Gateway for cryptographic functionality in type of a hardware security module with appropriate software installed. It provides an eternal communication interface to the Gateway, so that the cryptographic service functionality provided by the TOE can be utilized by the Gateway via this interface. Moreover, the TOE serves as a secure storage for cryptographic keys and certificates and further sensitive data relevant for the Gateway.

### TOE Physical Boundary
The TOE comprises the hardware and software that is relevant for the security functionality of the Security Module.
The Security Module is physically embedded into the Gateway and is therefore physically protected by the same level of physical protection as assumed for and provided by the environment of the Gateway.

### TOE Logical Boundary
The logical boundary of the Security Module (TOE) can be defined by its major security functionality:
- Digital Signature Generation
- Digital Signature Verification
- Key Agreement for [[TLS]]
- Key Agreement for Content Data Encryption
- Key Pair Generation
- Random Number Generation
- Component Authentication via the [[PACE]] Protocol with Negotiation of Session Keys
- Secure Messaging
- Secure Storage of Key Material and further data relevant for the Gateway
All these security features are used by the Gateway to uphold the overall security of the Smart Metering System.

### External Entities
| Subjects              | Role                                | Definition                                                                      |
| --------------------- | ----------------------------------- | ------------------------------------------------------------------------------- |
| External World        | User                                | Human or IT entity, possibly unauthenticated                                    |
| Gateway               | Authenticated Gateway               | Successful authentication via pace protocol between Gateway and TOE             |
| Gateway Administrator | Authenticated Gateway Administrator | Successful external authentication of the Gateway Administrator against the TOE |
### Threats

#### Side Channel and Fault Injection Acronyms
|Abbrev.|Full term|One‑line description|
|---|---|---|
|**SPA**|**S**imple **P**ower **A**nalysis|Reads the raw power‑consumption trace of a single operation and infers secrets from obvious patterns (e.g. different Hamming weights produce visible spikes).|
|**DPA**|**D**ifferential **P**ower **A**nalysis|Collects many traces, aligns them statistically and uses correlation/difference-of-means tests to extract sub‑keys that are _not_ visible with SPA alone.|
|**DFA**|**D**ifferential **F**ault **A**nalysis (or _attack_)|Intentionally injects faults (glitches, voltage/clock spikes, laser shots) during a crypto operation; compares correct vs. faulty outputs to solve for the secret key.|
|**SEMA**|**S**imple **E**lectro**m**agnetic **A**nalysis|Like SPA but observes the chip’s near‑field EM emissions instead of its power rail; useful when power probes cannot be inserted.|
|**DEMA**|**D**ifferential **E**lectro**m**agnetic **A**nalysis|The EM analogue of DPA: gathers many EM traces and applies statistical correlation to recover key bits.|
#### List of Threats

| Threat                   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Forge Internal Data      | An attacker with high attack potential tries to forge internal User Data or TSF Data via the regular communication interface of the TOE. This Threat comprises several attack scenarios of forgery of internal User Data or TSF Data. The attacker may try to alter User Data e.g. by deleting and replacing persistently stored key objects or adding data to data already stored in elementary files. The attacker may misuse the TSF management function to change the user authentication data (GW-PIN) to a known value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Compromise Internal Data | An attacker with high attack potential tries to compromise confidential User Data or TSF Data via the regular communication interface of the TOE. <br>This threat comprises several attack scenarios of revealing confidential internal User Data or TSF Data. The attacker may try to compromise the user authentication data (GW-PIN), to reconstruct a private signing key by using the regular command interface and the related response codes, or to compromise generated shared secret values or ephemeral keys.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Misuse                   | An attacker with high attack potential tries to use the TOE functions to gain access to access control protected assets without knowledge of user authentication data or any implicit authorization.<br>This threat comprises several attack scenarios. The attacker may try to circumvent the user authentication mechanism to access assets or functionality of the TOE that underlie the TOE's access control and require user authentication. The attacker may try to alter the TSG data e.g. to extend the user rights after successful authentication.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Intercept                | An attacker with high attack potential tries to intercept the communication between the TOE and the Gateway to disclose, to forge or to delete transmitted (sensitive) data or to insert data in the data exchange.<br>This threat comprises several attack scenarios. An attacker may read data during data transmission in order to gain access to user authentication data (GW-PIN) or sensitive material as generated ephemeral keys or shares secret values. An attacker may try to forge public keys during their import to respective export from the TOE.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Leakage                  | An attacker with high attack potential tries to launch a cryptographic attack against the implementation of the cryptographic algorithms or tries to guess keys using a brute-force attack on the function inputs.<br>This threat comprises several attack scenarios. An attacker may try to predict the output of the random number generator in order to get information about a generated session key, shares secret value or ephemeral key. An attacker may try to exploit leakage during a cryptographic operation in order to use SPA, DPA, DFA, SEMA or DEMA techniques with the goal to compromise the processed keys, the GW-PIN or to get knowledge of other sensitive TSG or User data. Furthermore an attacker could try guessing the processed key by using a brute-force attack. in addition, timing attacks have to be taken into account.<br>The sources for this leakage information can be the measurement and analysis of the shape and amplitude of signals or the time between events found by measuring signals on the electromagnetic field, power consumption, clock, or I/O lines (side channels). |
| Physical Tampering       | An attacker with high attack potential tries to manipulate the TOE through physical tampering, probing or modification in order to extract or alter User Data or TSF Data stored in or processed by the TOE. Alternatively, the attacker tries to change TOE functions (as e.g. cryptographic functions provided by the TOE) by physical means (e.g. through fault injection).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Abuse Functionality      | An attacker with high attack potential tries to use functions of the TOE which shall not be used in TOE operational phase in order (i) to disclose or manipulate sensitive User Data or TSF Data, (ii) to manipulate the TOE's software or (iii) to manipulate (explore, bypass, deactivate or change) security features or functions of the TOE.<br>In particular, the TOE shall ensure that functionality that shall not be usable in the operational phase, but which is present during the phase of the TOE's manufacturing and initialization as well as during the integration phase of the Gateway and the TOE, is deactivated before the TOE enters the operational phase. Such functionality includes in particular testing, debugging and initialization functions.                                                                                                                                                                                                                                                                                                                                               |
| Malfunction              | An attacker with high attack potential tries to cause a malfunction of the TSF or of the IC Embedded Software by applying environmental stress in order to (i) deactivate or modify security features or functions of the TOE or (ii) circumvent or deactivate or modify security functions of the IC Embedded Software.<br>This may be achieved e.g. by operating conditions, exploiting errors in the IC Embedded Software or misuse of administration function. To exploit this an attacker needs information about the functional operation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

## Rationale for Security Objectives
![[Screenshot 2025-04-22 at 14.46.14.png]]![[Screenshot 2025-04-22 at 14.46.35.png]]

### Cryptographic Support
The Security Module serves as a cryptographic service provider for the Smart meter Gateway and provides services in the following cryptographic areas:
- Signature Generation ([[ECDSA]])
- Signature Verification (ECDSA)
- Key Agreement for TLS (ECKA-DH)
- key Agreement for Content Data Encryption (ECKA-DH)
- Key Pair Generation
- Random Number Generation
- Component Authentication via the PACE Protocol with Negotiation of Session Keys ([[PACE]])
- Secure Messaging
- Secure Storage of Key Material and further data relevant for the Gateway.