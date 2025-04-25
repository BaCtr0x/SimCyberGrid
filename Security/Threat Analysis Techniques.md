## Workflow
Before we start it is important to note that the threat analysis is often done through the eyes of an attacker and not from the viewpoint of a defender. This helps to identify potential points of entry and allows one to make threat modeling a core component of the software developer life cycle (SDLC). For us we need to make sure that we identify and model as many attacks as possible, in order to identify critical points of attack and thus determine which attacks we want to test on the final simulation. This document follows the guidlines of OWASP.
### 1. Scope Work
In this step we need to gain information and understand what the application of our work is supposed to do and how it will be done. For this we call use the following tools:
- Drawing diagrams, most useful is the Data Flow Diagram (DFG)
- Identifying entry points to see where a potential attacker could interact with the application
- Trying to identify "assets"
- Identify trust levels that represent the access right that the application will grant to external entities
### 2. Determine Threats
In this step we use a threat categorization methodology to identify threats. For this one could use the following thread modeling techniques, depending on the application one want to use.
#### Threat Modeling Techniques

| Model                      | Domain Fit      | Visual | Quantitative | Physical Threats | Complexity | Tool Support      |
| -------------------------- | --------------- | ------ | ------------ | ---------------- | ---------- | ----------------- |
| **STRIDE**                 | Cyber + grid    | ✔️     | ❌            | ❌                | Low        | Microsoft TMT     |
| **PASTA**                  | Cyber-physical  | ✔️     | ✔️           | ⚠️ Partial       | High       | Manual / Custom   |
| **MITRE ATT&CK ICS**       | ICS/OT-specific | ❌      | ⚠️ Tactical  | ❌                | Medium     | ATT&CK Navigator  |
| **Attack Trees**           | All domains     | ✔️     | ⚠️ Custom    | ✔️               | Medium     | Tree tools, paper |
| **Risk Matrix (IEC/NIST)** | Grid-focused    | ⚠️     | ✔️           | ✔️               | Low-Med    | Compliance tools  |
In this context we note that combining different threat modeling techniques can be useful, such as using STRIDE in combination with the attack trees to model different points of entry and give detailed attack strategies for the most relevant attacks or in our case the ones we want to test on the simulator. Additionally it is helpful to use the DFG to identify threat boundaries and document them in the DFG such that one can easily get an overview of the different points of entries. For us this is going to be a little bit more difficult, as most attacks we will be looking at will focus on destabilizing the grid, which is the result of the attack and not the attack itself. 
### 3. Determine Countermeasures and Mitigation
The idea behind this step is to identify countermeasures to the attacks found in the previous step. For this one could use threat-countermeasure mapping lists. The most common factors in the counter-measurement analysis is to determine factors of the attacks like:
- the attack itself
- the damage of the attack
- the complexity of the attack
- and the cost to fix the damage done

For the risk mitigation strategies one can go ahead and evaluate the threats and their impact and then decide on a business level what to do. Once the impact is identified one could do the following:
- **Accept:** decide that the business impact is acceptable and document who has chosen to accept the risk
- **Eliminate:** remove components that make the vulnerability possible
- **Mitigate:** add checks or controls that reduce the risk impact, or the chances of its occurrence
- **Transfer:** Transfer risk to an insurer or customer

### 4. Assess your work
The final step is to asses the work you have done and determine whether there are any missing parts or if everything is covert. This process will be repeated in the SDLC to incorporate additional threats or vulnerabilities found in the development process or through new scientific advancements and research that shows previously unknown attack vectors, such as the backdoor in GEA-1 shown in: [[GAE-1 and GAE-2 Cryptanalytic Attacks Overview]].


## Our Approach
I would recommend we utilize risk matrices as they are quantitative, incorporate physical threats and are not that complex and difficult to create. To get an additional vector of visualization and to define the attack vectors, with their mode of operation and their impact we should combine the risk matrices with attack trees. These are a great bases to give additional information about the attack context and to give background information about why which entry was chosen in the risk matrix.

### Why Combine Risk Matrices with Attack Trees?
Risk matrices help you to:
- Prioritize asses-threat combinations
- Communicate risk levels to stakeholders
- Align with compliance (e.g. NIST SP 800-30, NISTIR 7628, IEC 62443)

Attack Trees help us to:
- Understand attack paths and conditions
- Visualize multi-step, cascading, or coordinated attacks
- Support "what-if" analysis of mitigations or controls

Thus combining both gives one the ability to prioritize attacks while having a tactical modeling of the attacks.

### Workflow
1. Build Attack Trees per asset or threat scenario
	- Root = attack goal (e.g. "Disable DER Controller")
	- Leaves = preconditions (e.g. credentials, remote access)
2. Evaluate each path for Impact + Likelihood
	- Use results to populate the matrix
3. Prioritize mitigations based on:
	- How many high-risk branches pass through each node
	- What controls can reduce likelihood or break attack paths