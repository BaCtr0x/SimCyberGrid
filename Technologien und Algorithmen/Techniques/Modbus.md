Modbus is an **application-layer protocol** that allows devices on industrial networks to communicate with each other. It's primarily used in **SCADA systems** and **industrial automation environments** to transmit data between **control systems and field devices**.

### **Common Modbus Device Types**
- **Modbus RTU Devices**  
    Communicate over **serial lines** (RS-232 or RS-485)  
    Binary data format, efficient and compact
- **Modbus TCP Devices**  
    Communicate over **Ethernet networks**  
    Based on TCP/IP, used in modern industrial networks
- **Modbus ASCII Devices**  
    Also serial, but use ASCII encoding (less efficient)

### **Security Note**
Modbus, especially Modbus RTU and Modbus TCP, was designed for **reliability and simplicity**, not security. It lacks:
- Encryption
- Authentication
- Integrity checks
As such, **Modbus devices are often vulnerable** to attacks if not properly segmented from external networks.