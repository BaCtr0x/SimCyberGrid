Eine **CRL** ist eine Liste von X.509-Zertifikaten, die frühzeitig für ungültig erklärt wurden („revoked“), bevor ihr eigentliches Ablaufdatum erreicht ist.

- **Wer erstellt sie?**  
    - Die **Issuing CA** (Zertifizierungs­stelle) stellt regelmäßig eine neue CRL aus und signiert sie.

- **Was steht drin?**  
    - Seriennummer jedes widerrufenen Zertifikats
    - Widerrufsdatum  
    - (Optional) Widerrufsgrund (KeyCompromise, CessationOfOperation, etc.)

- **Wozu dient sie?**  
    - Clients (z. B. SMGW, SCADA-Gateway) laden die CRL periodisch herunter und verifizieren beim TLS-Handshake, ob das Gegenstellen-Zertifikat noch gültig ist. Ist die Seriennummer in der CRL gelistet, wird die Verbindung abgelehnt.