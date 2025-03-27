## Requirement Standards Considered (The 'What')

| **Standard**     | **Beschreibung**                                                                                                                                                                  | **Dokument** |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| ISO/IEC 15408    | Information security, cybersecurity and privacy protection - Evaluation criteria for IT security                                                                                  | SGCG         |
| ISO/IEC 18045    | Information security, cybersecurity and privacy protection - Evaluation criteria for IT security - Methodology for IT security evaluation                                         | SGCG         |
| ISO/IEC 19790    | ~~Information technology - Security techniques - Security requirements for cryptographic modules~~ [Withdrawn]                                                                    | SGCG         |
| ISO/IEC TR 27019 | ~~Information technology - Security techniques - Information security controls for the energy utility industry~~ [Withdrawn]                                                      | SGCG         |
| IEC 62443-2-4    | Security for industrial automation and control systems - Network and system security - Part 2-3: Requirements for Industrial Automation Control Systems (IACS) solution suppliers | SGCG         |
| IEC 62443-3-3    | Security for industrial automation and control systems, Part 3-3: System security requirements and security levels                                                                | SGCG         |
| IEC 62442-4-2    | Security for industrial automation and control systems, Part 4-2: Technical Security Requirements for IACS Components                                                             | SGCG         |
| IEC 62443-2-1    | Security for industrial automation and control systems - Network and system security - Part 2-1: Industrial automation and control system security management system              | SGCG         |
| IEEE 1686        | Substation Intelligent Electronic Devices (IED) Cyber Security Capabilities                                                                                                       | SGCG         |
| IEEE C37.240     | Cyber Security Requirements for Substation Automation, Protection and Control Systems                                                                                             | SGCG         |

### ISO/IEC 15408 – Common Criteria for Information Technology Security Evaluation

**Detailed Description:**  
ISO/IEC 15408 defines a framework for evaluating the security properties of IT products and systems, commonly known as **Common Criteria (CC)**. It includes **Protection Profiles (PPs)**, **Security Targets (STs)**, and **Evaluation Assurance Levels (EALs)**, ranging from 1 (basic) to 7 (formally verified design and testing). It ensures consistency and comparability of evaluations and is widely accepted for certification globally.

---
### ISO/IEC 18045 – Evaluation Methodology for IT Security

**Detailed Description:**  
This standard is the companion to ISO/IEC 15408 and specifies the **methodology for conducting evaluations** of IT security as defined in the Common Criteria. It outlines how to verify that a system meets the requirements in a Protection Profile or Security Target, and guides evaluators through assurance activities and evidentiary assessments.

---
### ~~ISO/IEC 19790 – Security Requirements for Cryptographic Modules~~ [Withdrawn]

**Detailed Description:**  
ISO/IEC 19790 defines security requirements for **cryptographic modules**, similar to **FIPS 140-3**. It categorizes requirements into areas like physical security, roles and services, key management, and self-tests. It defines four increasing **security levels (1–4)** and ensures cryptographic modules are properly designed, implemented, and tested.

---
### ~~ISO/IEC TR 27019 – Information Security for Energy Utility Automation Systems~~ [Withdrawn]

**Detailed Description:**  
This is a **technical report** providing guidelines based on ISO/IEC 27002, tailored to **energy utility automation** systems like SCADA and industrial control. It extends general information security controls to address the specific operational, technical, and environmental risks in energy sector ICS/OT environments.

---
### IEC 62443-2-4 – Requirements for IACS Service Providers

**Detailed Description:**  
Part of the IEC 62443 series focused on **Industrial Automation and Control Systems (IACS)** security. This part defines cybersecurity requirements for **service providers** (e.g., system integrators, maintenance providers), ensuring secure integration, delivery, and support of IACS solutions.

---
### IEC 62443-3-3 – System Security Requirements and Security Levels

**Detailed Description:**  
Outlines detailed **security requirements at the system level** and defines **seven foundational requirements**, such as access control and data integrity. Introduces **Security Levels (SL 1–4)** for systems, supporting defense-in-depth architectures in ICS environments.

---

### IEC 62443-4-2 – Technical Security Requirements for IACS Components

**Detailed Description:**  
Focuses on **technical security requirements** for individual components (e.g., PLCs, HMIs, sensors) in IACS environments. It complements 4-1 (secure development lifecycle) and supports mapping to system-level requirements from 3-3, enforcing security at the **component level**.

---

### IEC 62443-2-1 – Security Program Requirements for Asset Owners

**Detailed Description:**  
This part defines how asset owners (e.g., plant operators) should establish and maintain a **cybersecurity management system (CSMS)**. It outlines processes like risk assessment, policies, training, and incident response tailored to industrial environments.

---
### IEEE 1686 – Substation Intelligent Electronic Devices (IED) Cybersecurity Capabilities

**Detailed Description:**  
Specifies cybersecurity features that should be supported by **IEDs in substations**, such as role-based access control, logging, secure communication, and firmware integrity. It’s focused on **substation automation and grid resilience** through secure device design.

---
### IEEE C37.240 – Cybersecurity for Protection and Automation of Power System Substations

**Detailed Description:**  
Provides **cybersecurity best practices** for protection and automation systems in power substations. It addresses threat modeling, risk assessment, and mitigation strategies, focusing on interoperability, resiliency, and NERC-CIP alignment.


---

## Solution Standards Considered (The 'How')

| **Standard**                    | **Beschreibung**                                                                                                                   | **Dokument** |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| ISO/IEC 15119-2                 | Defines secure app-layer protocols for EV-to-charger comms incl. Plug & Charge and [[TLS]]-based auth.                             | SGCG         |
| IEC-62351-x                     | Security extensions for power system protocols; covers TLS, [[Role-Based Access Control\|RABAC]], certs and secure key management. | SGCG         |
| IEC 62056-5-3                   | Smart metering app-layer protocol for secure DLMS/COSEM data exchange; supports auth/encryption.                                   | SGCG         |
| IETF RFC 6960                   | Enables real-time X.509 cert status checks via HTTP; faster alternative to CRLs                                                    | SGCG         |
| IETF RFC 7252                   | Lightweight RESTful protocol for IoT over UDP; supports DTLS for security.                                                         | SGCG         |
| IETF draft-weis-gdoi-iec62351-9 | Draft for using GDOI to manage group keys in IEC 62351-9 for multicast comms in power systems.                                     | SGCG         |
| IETF RFC 7030                   | Secure X.509 cert enrollment protocol over HTTPS with TLS-based auth and rekeying.                                                 | SGCG         |

### ISO/IEC 15118-2 – Vehicle-to-Grid Communication Interface: Network and Application Protocol Requirements

**Detailed Description:**  
Part of the ISO 15118 series, this standard defines **network and application-layer protocols** for communication between **electric vehicles (EVs)** and **charging stations** (EVSE). It supports **Plug & Charge**, secure mutual authentication using X.509 certificates, and encrypted communication via TLS. It is foundational for smart charging and V2G integration.

---
### IEC 62351-x – Power System Information Security

**Detailed Description:**  
A multi-part standard series focused on securing communication protocols used in **power system automation** (e.g., IEC 60870-5-104, IEC 61850). It includes security for transport layers (TLS, SSH), role-based access control, certificate handling, and intrusion detection. Each part (e.g., 3, 4, 5, 9) covers specific technical layers.

---
### IEC 62056-5-3 – DLMS/COSEM Application Layer Protocol

**Detailed Description:**  
Defines the **application layer** of the DLMS/COSEM suite used for **smart metering**. It supports secure messaging, association control, and data exchange via APDUs. Includes support for cryptographic protection (authentication, encryption) and defines OBIS codes for object modeling.

---

### IETF RFC 6960 – Online Certificate Status Protocol (OCSP)

**Detailed Description:**  
Defines OCSP for obtaining **real-time certificate revocation status** from a certificate authority (CA). More efficient than CRLs, OCSP enables clients to query the validity of X.509 certificates via HTTP without downloading large lists. It supports signed responses for integrity and freshness.

---
### IETF RFC 7252 – Constrained Application Protocol (CoAP)

**Detailed Description:**  
CoAP is a lightweight, RESTful protocol for **resource-constrained devices** in IoT environments. It operates over UDP and supports DTLS for secure communication. CoAP mirrors HTTP verbs (GET, POST) but with a smaller footprint and is well-suited for sensor networks and constrained nodes.

---
### IETF draft-weis-gdoi-iec62351-9 – GDOI-Based Key Management for IEC 62351-9

**Detailed Description:**  
This IETF draft proposes using **GDOI (Group Domain of Interpretation)** for **group key management** as specified in IEC 62351-9. It defines protocols for securely distributing symmetric keys to authorized entities in power systems using multicast security, authentication, and rekeying mechanisms.

---
### IETF RFC 7030 – Enrollment over Secure Transport (EST)

**Detailed Description:**  
EST defines a certificate enrollment protocol over **HTTPS**, serving as a modern, secure replacement for SCEP. It supports TLS client authentication, renewal, and rekeying of X.509 certificates. EST is extensible and integrates with PKI environments in secure automation and IoT deployments.