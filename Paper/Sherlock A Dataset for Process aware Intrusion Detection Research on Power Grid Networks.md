The paper "Sherlock: A Dataset for Process-aware Intrusion Detection Research on Power Grid Networks" by Eric Wagner et al. introduces Sherlock, a comprehensive dataset designed to facilitate research on intrusion detection systems (IDS) tailored for power grids. The dataset is generated using the Wattson co-simulator, which provides realistic simultaneous simulation of power grids and their associated ICT networks. Sherlock covers multiple scenarios representing different grid complexities with detailed network captures, process state logs, and ground truth data on cyberattacks.

## Summary
- Sherlock addresses the critical lack of high-quality, publicly available datasets integrating both network and physical process data for power grid cybersecurity.
- The dataset captures attacks affecting the physical process state, such as injecting malicious commands or manipulating measurements.
- Three scenarios of varying scale are included: a basic scenario based on the CIGRE reference grid, a semiurban scenario using Simbench data, and a rural scenario.
- The dataset supports passive monitoring from multiple vantage points to reflect real-world, non-invasive deployments.
- The authors benchmark five recent industrial IDSs on Sherlock, revealing significant challenges such as distinguishing benign anomalies caused by maintenance, scalability across large networks, and the need for multi-layer detection approaches.
- Six major challenges for IDS research in power grids are identified, ranging from data volume and training limitations to the complexity of benign anomalies and the importance of combining process-aware, network-, and host-based IDS techniques.

## Simulator Frameworks Used

- **Wattson Co-simulator**: The cornerstone simulation framework for Sherlock, Wattson integrates:
    - **PowerOwl** for power grid modeling, which is based on pandapower for steady-state power flow calculations.
    - Realistic ICT network emulation using containerized lightweight namespaces and Linux tools for simulating routers, switches, hosts, and communication properties such as delay, jitter, bandwidth, and packet loss.
    - Emulation of protocols such as IEC 60870-5-104, commonly used in power grid substation control.
    - Real-time co-simulation with accelerated power profile simulation that enables generating large amounts of data over extended simulated periods.
    - Support for hardware-in-the-loop experiments for validation.
- Wattson simulates interactions between the physical electrical grid and its control and communication networks, enabling realistic attack scenario replication and the creation of comprehensive datasets integrating network traffic and physical process data.

In summary, Sherlock leverages Wattson's dual-domain power and ICT co-simulation capabilities to generate highly realistic, scalable, and well-documented datasets vital for advancing process-aware intrusion detection in electrical power grids