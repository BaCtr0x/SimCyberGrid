Security Assertion Markup Language is a federated identity protocol used for Single Sign-On (SSO), especially in enterprise and cloud environments (like Microsoft 365, AWS, Salesforce)

## How SAML Works (High-Level Flow)
SAML allows a user to log into multiple services using one identity provider (IdP).
1. User attempts to access a service (e.g. Microsoft 365)
2. The Service Provider (SP) redirects the user to the Identity Provider (e.g. ADFS)
3. The IdP authenticates the user (with username/password or MFA)
4. The IdP sends a signed SAML assertion (XML token) back to the SP
5. The SP accepts the token and grants access

## SAML Assertion (The Token)
- XML format
- Contains:
	- User identity
	- Group membership
	- Validity period
- Digitally signed by the IdP using a private key
Example snippte:
```XML
<Assertion>
  <Subject>
    <NameID>alice@corp.local</NameID>
  </Subject>
  <AttributeStatement>
    <Attribute Name="Role">Admin</Attribute>
  </AttributeStatement>
</Assertion>
```

## Golden SAML Attack
Just like a Golden Ticket in Kerberos, attackers can create forged SAML tokens:
	Golden SAML = custom-generated SAML assertion, signed with the IdP's stolen private key

### Steps
1. attacker compromises ADFS or IdP server
2. Extracts the SAML token-signing private key
3. Generates arbitrary SAML assertions:
	- Any user identity
	- Any roles or groups
	- Long expiry
4. Submits token directly to the cloud service
This allows access without passwords, MDA, or logs in the IdP, because the IdP never saw the request - the token is inserted directly at the SP.
### Tools Used:
- TokenForge
- ADFSDump
- [[Mimikatz]] (to extract key via `lsadump::lsa /inject`)

## Impact
- Works even after passwords are reset
- MFA cannot protect against it
- Full access to cloud environments (Exchange Online, SharePoint, Azure AD)
- Often persists after initial breach is remediated, unless token-signing certs are rotated

## Detection & Defense Summary
|Threat|Detection|Mitigation|
|---|---|---|
|Mimikatz|Unusual LSASS access; memory inspection; EDR alerts|Enable LSA protection; restrict admin rights; AV signatures|
|Golden Ticket|Unusual ticket lifetimes; service tickets for nonexistent users|Rotate KRBTGT twice; monitor Kerberos ticket anomalies|
|Golden SAML|Long-lived SAML tokens; SSO logins bypassing IdP|Rotate ADFS token-signing certs; monitor SP login behavior|