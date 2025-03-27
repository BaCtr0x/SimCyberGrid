## Security Levels
![[SGIS_Levels.png]]

They use the SGIS - Security Levels (SGIS-SL) to create a bridge between the electrical grid and the information security. This security levels in their definition do not really apply to us as we are operating in the middle to low power range and thus in the low to Medium, maybe High security level. In addition to this they follow the idea that they follow a list of standards provided by the European set of recommendations. These standards are clustered into requirement standards and solution standards, listed and described in [[Sicherheitsstandards]]. 

## Standard Mapping
These standards are then mapped to $4$ standards areas in the next figure. These areas are:
- **Details for Operation:** The standard addresses organizational and procedural means applicable for all or selected actors. It may have implicit requirements for systems and components without addressing implementation options.
- **Relevance for Products:** The standard directly influences component and/or system functionality and needs to be considered during production design and/or development. it addresses technology to be used to integrate a security measure.
- **Design Details:** The standard describes the implementation of security means in details sufficient to achieve interoperability between different vendor's products for standards on a technical level and/or procedures to be followed for standards addressing organizational means.
- **Completeness:** The standard addresses not only one specific security measure but addresses the complete security framework, including technical and organizational means.

![[Security_Standard_Coverage.png]]


## Mapping Requirement Standards to SGAM
They then map the standards to the SGAM model, which is rather long due to many standards, which is why I will not include it in here, but rather just give the corresponding page to start from: $17$.

## Mapping to Use-Cases:
At first it is important to note that the Use-Cases they are talking about here are not the same as defined in the first document. Here they simply list $4$ Use-Cases, which are more like a focus on different domains in the SGAM model.
- UC1: Transmission Substation
- UC2: Distribution Control Room
- UC3: Flexible and Consumer Demand Management
- UC4: Distributed Energy Resources (DER) Control
They do this because these Use-Cases have already been analyzed and provide sufficient room to analyze all standards without the need to define additional Use-Cases.

## European Set of Recommendations Overview
In April 2014, ENISA and European Commission Smart Grid Task Force Expert Group 2 (EG2) ad hoc group, release a "Proposal for a list of security measures for Smart Grids" report, this defines many security measures in combination with standards. 
You can find additional information about critical infrastructure and cybersecurity here: [Critical Infrastructure and Cybersecurity](https://energy.ec.europa.eu/topics/energy-security/critical-infrastructure-and-cybersecurity_en) 
Here is an overview from the SGIS document:
![[European_set_of_recommendations_domain_overview.png]]


## Privacy Protection
They describe the importance of privacy protection and mention the European Commission data protection regulation which has a significant impact on privacy protection, however they do not talke about specific attack on privacy that relate specific to smart grids but rather enter the general field of communication network attacks and the result of inadequate anonymization. 

Furthermore, they state the following $5$ privacy protection principles:
- Privacy by Design
- Privacy Enhancing Technologies
- Challenges in Anonymization
- Smart Grid Data Sources and Risks
- Data Protection Impact Assessment

