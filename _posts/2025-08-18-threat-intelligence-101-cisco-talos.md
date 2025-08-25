 ---
layout: post
title: "Cisco - Threat Intelligence 101 with Cisco Talos"
date: 2025-08-18
categories: [blog]
 ---
 
# Title  
Threat Intelligence 101 with Cisco Talos
 
What did I learned from this course?

- How information is used to make strategic decisions. 

We need to understand the technology, its capacities, and weaknesses to protect the systems, the technological assets, and the information.
 
There is the knowledge management pyramid, which helps us to achieve this goal. It helps us to understand the path process from collected data till it is converted in wisdom throughout the information and knowledge phases.
- Wisdom -> understanding of why and how things need to be done 
- Knowledge -> information that is understood and contextualized with other learning and experience  
- Information -> data that is summarized, structured with added context 
- Data -> facts, measurements, observables

We can classify threat intelligence into the next three types:
- Strategic
- Operational
- Tactical

Threat actors are classified as:
- Cyber criminal 
- Nation-state 
- Ideologues 
- Thrill seekers 
- Insiders

Patters (TTPs) -> These are related to the ATT&CK Framework 
- Techniques 
- Tactics
- Procedures 

The curse teaches us about the intelligence cycle. It has to be used as a guide, but not considered as something immutable.

The cycle has different stages:
- Planning & Direction
- Data collection
- Processing
- Analysis
- Production
- Dissemination

The majority of the course ramarks the relevance of apply a serie of steps to transform data into useful information to take decisions.  

As the course progressed, I learned with respect to the "See it, Sense it, Share it, and Use it" model, designed for rapid sharing and practical use of intelligence within the private sector, focusing on quick interpretation and dissemination of data.

Other models are mentioned as:

- F3EAD (Find, Fix, Finish, Exploit, Analyse, and Disseminate)
- D3A (Decide, Detect, Deliver, and Assess)

There is a measure to estimate the validity of the data, and it  works with three levels:
- Low (Poor data)
- Medium (Partial corroboration from good sources)
- High (Good information from good sources)

A key point at the moment to write a report is to consider the audience's needs, separate facts from points of view.

For that aim, the course presents the Traffic Light Protocol (TLP)
- Red (no disclosure)
- Amber (limited disclosure)
- Green (disclosure within the community)
- White (no disclosure limitations)

Threat Hunting concept: Based on the search for information and evidence to inform those who are the decision makers. Focused on investigation. 

Threat Hunting Loop  
- Create Hypothesis 
- Investigate (Find the indicator)  
- Uncover (discover additional indicators) 
- Inform & Enrich (Provide situational awareness or resolution advice)

Logs Security Tools are a crucial part of this area.

The information collection is the key, then analyze and identify.

V Diagram Model 
- Characterize activity 
- Develop hypotheses.                      ——> characterization phase 
- Determine data requirements 
- Implement tests 
- Formulate conclusions                    ——> execution phase 
- Update activity characterization   

The investigation process: Require the evidence analysis before stating any kind of hypothesis.
- Confirmation Bias 
- Anchoring Bias
- Apophenia 
- Agent Bias
 
Attribution: Investigación de cyberattacks to identify who or whose are the attack responsables 

TTP’s identifications, tools, and who or whose were the attack objective, all that knowledge works to anticipate future attacks.   

I learned concepts related to the Kill Chain, which is a model that is used to define the 7 steps of a cyberattack:
- Reconnaissance (research, identify)
- Weaponization (prepare payload)
- Delivery (Transmit payload)
- Explotation (Exploit vulnerability)
- Installation (Install payload)
- Command & Control (establish communication)
- Actions on Objective (Fulfill goals of attack)

Diamond Model 
-> Victim -> subjected to -> Attacker Capabilities -> Deploys ->
-> Threat actor -> Uses -> Malicious Infraestructure -> Connects to -> Victim ->

Example attack Attributes 
- Techniques                      Victimology
- Tactics                         Ransom
- Procedures                      Time & Data
- Lolbins                         Malware type          Hash Value
- Language use                    Files                 Metadata                                              Domain name 


I conclude that we don’t need to trust in the information that we hear or we read beacuse it could be put in with the intention that create confusion, we need to have a criteria to filter and corroborated the information, create suppositions. It is the opposite that we need to do, and for that reason, there are many frameworks and methods to help us with that.



25 August 2025
[J x 2] 

 
---

[← Volver al inicio]({{ "/" | relative_url }})
