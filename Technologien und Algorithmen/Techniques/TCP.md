**TCP (Transmission Control Protocol)** ist ein verbindungsorientiertes Transportprotokoll, das auf IP aufsetzt und folgende Kernfunktionen bietet:

1. **Verbindungsaufbau (Three-Way Handshake)**
    1. **SYN**: Der Client schickt ein Segment mit dem SYN-Flag und seiner Initial Sequence Number (ISN).
    2. **SYN+ACK**: Der Server antwortet mit SYN+ACK, bestätigt die Client-ISN (Seq+1) und sendet seine eigene ISN.
    3. **ACK**: Der Client bestätigt die Server-ISN (Seq+1).  
        Erst jetzt ist die TCP-Verbindung etabliert und Datenübertragung möglich.

2. **Zuverlässigkeit & Reihenfolge**    
    - **Sequenznummern** (32 Bit) markieren jedes Byte im Datenstrom.
    - **ACK-Nummern** bestätigen den Erhalt bis zu einer bestimmten Byte-Nummer (cumulative ACK).
    - **Retransmission**: Fehlende ACKs innerhalb eines Retransmission-Timeouts (RTO) lösen die erneute Aussendung aus.
    - **In-Order Delivery**: Eingehende Segmente werden gepuffert und in korrekter Reihenfolge an die Anwendung übergeben.

3. **Flusskontrolle**    
    - **Receive Window** (rwnd): Der Empfänger gibt laufend an, wie viele Bytes Puffer er noch frei hat.
    - Der Sender darf niemals mehr unbestätigte Bytes senden, als das aktuelle rwnd erlaubt.

4. **Staukontrolle (Congestion Control)**    
    - **Slow Start**: Beginn mit einem kleinen Congestion Window (cwnd), das bei jedem ACK exponentiell wächst.
    - **Congestion Avoidance**: Nach Erreichen der Slow-Start-Schwelle (ssthresh) wächst cwnd linear.
    - **Fast Retransmit & Fast Recovery**: Bei drei aufeinanderfolgenden Duplicate ACKs wird ein Paket als verloren angesehen und sofort neu gesendet; cwnd wird halbiert, dann vorsichtig wieder erhöht.

5. **Verbindungsabbau (Four-Way Teardown)**    
    1. Ein Ende schickt **FIN** → das andere Ende ACKt.
    2. Danach sendet dieses zweite Ende selbst FIN → erste Seite ACKt.
    3. Beide Seiten gehen in TIME_WAIT, um verspätete Segmente im Netz auszuschließen.

6. **Multiplexing über Ports**    
    - TCP-Header enthält **Quell-Port** und **Ziel-Port** (je 16 Bit), womit mehrere Verbindungen zwischen denselben Hosts unterschieden werden.

7. **Header-Optionen**    
    - **MSS** (Maximum Segment Size), **Window Scale**, **Timestamps**, **Selective Acknowledgment (SACK)** für verbesserte Leistung und Flexibilität.


---

> **Kurz:** TCP realisiert über **Handshake**, **Sequenzierung**, **ACKs**, **Window-Mechanismen** und **Staukontrolle** einen zuverlässigen, geordneten, fluss- und stau­geregelten Byte-Strom über ein unzuverlässiges IP-Netz.