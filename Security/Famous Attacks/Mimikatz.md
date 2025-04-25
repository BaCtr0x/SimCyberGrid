Mimikatz is an open-source post-exploitation tool. It's often seen in red team ops and real-world breaches due to its powerful capabilities for credential harvesting and privilege escalation.

## What is does
|Feature|Description|
|---|---|
|**LSASS Dumping**|Extract plaintext passwords, hashes, Kerberos tickets from memory|
|**Pass-the-Hash (PtH)**|Reuse NTLM hashes without knowing the plaintext password|
|**Pass-the-Ticket (PtT)**|Inject Kerberos TGT/TGS tickets into a session|
|**Overpass-the-Hash**|Use NTLM hash to request Kerberos TGT|
|**Kerberos Ticket Forgery**|Create _golden_ or _silver_ tickets|
|**Credential Delegation Abuse**|Abuse cached delegated credentials (RDP, WMI)|
## How it Works
- Mimikatz interacts with lsass.exe (Local Security Authority Subsystem Service)
- LSASS holds credentials in memory: plaintext, NTLM hashes, Kerberos tickets
- Admin-level access is required (often via privilege escalation or lateral movement)
- Example
```
mimikatz # sekurlsa::logonpasswords	
```
	Returns
		- Username
		- Domain
		- Password (plaintext or hash)
		- Logon type/session

## Golden Ticket via Mimikatz
A Golden Ticket is a forget Kerberos TGT (Ticket Granting Ticket)
- attacker dumps the KRBTGT account hash from a domain controller
- Uses Mimikatz to forge a valid TGT for any user, any group, with arbitrary expiration
- Can impersonate a Domain Admin indefinitely
```
kerberos::golden /user:admin /domain:corp.local /sid:S-1-5-21-... /krbtgt:<NTLM hash>
```

