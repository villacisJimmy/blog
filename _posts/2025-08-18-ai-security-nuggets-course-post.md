 ---
layout: post
title: "Cisco - AI Security Nuggets"
date: 2025-08-18
categories: [blog]
 ---
 
 # Title  
 Cisco - AI Security Nuggets 
 
This course is a short introduction to AI with a focus on cybersecurity. 

What I learned:

Technology is part of our lives, and it is going to continue being much more through over time. For anyone, nowadays, the concept of AI is not something new. We can see the economic benefits and some consequences, and it is for that reason that we mention the concept of "Dual-nature of technology.".

What it means "Dual-nature of technology"? Well, there are the pros and cons. AI is creating new economies, but the counterparty is that at the same time is creating new security gaps. More technology more exposed we are to people with bad intentions. AI is givin us the opportunity to put all our ideas in action, but in the same way that someone can use a gun to protect can use a gun to make a crime. 

The good news are that exist a large group of people dedicating time to solve this new challenges, you need to understand something behind the technology there are companies or people like us with there own ineterests and bias, and all that is transferred to this new techonolgy.

Countries know about this and they are implementing measures like “America’s AI Action Plan that has three pillars: innovation, infrastructure, and international diplomacy and security”.

The purpose of all is to create regulation in mitigating risk, but giving enough flexibility for adoption.

Companies like Cisco are taking action, for example Cisco is implementing the "Principles for Responsible Artificial Intelligence (transparency, fairness, accountability, privacy, security and reliability).

The United States has legislation in progress. The Artificial Intelligence Act, the first binding worldwide horizontal regulation on AI, sets a common framework for the use and supply of AI systems in the European Union.

The course mention the implementation of guidelines for secure AI system development. The AI system development life cycle has in consideration a secure design, secure development, secure deployment, and secure operation and maintenance. We can not forget that when we talked about "AI" we are talking about code, all thes algortims has similar prodecures than when we are creating a pice of software, but with much more complexity behind.

What is the result of the AI adoption from a cybersecurity perspective?. The answer it is not possible to keep using traditional systems to defend our networks against AI techniques.

For those who are familiarised with the OSINT concept, already exists the AI large-scale OSINT reconnaissance, which gives us the possibility of creating automatic social engineering attacks.

As I mentioned before, when we talked about AI we are talking about code and one of the biggest representatives in this topic is "OWASP" who is present with OWASP top 10 for LLM applications.

- Promp injection
- Insecure output handling
- Training data poisoning
- Model denial of service
- Supply chain vulnerabilities
- Sensitive information diclosure
- Insecure plugin desing
- Excessive agency
- Overreliance
- Model Theft

We need to know that models could potentially manipulated having as a result different biases and even security vulnerabilities.

The course metion that information as something extremely important nowadays and introduce the concepts like "artificial intelligence bill of materials or AI bombs", that are used to ensure transparency and traceability as part of the "AI Supply Chain Security".

SBoM is basically the list of ingredients that make up any software. However, we have to go a little bit, deeper. We have to think about the moral details, including versions and the provenance of the model and, the architecture of the model, including the parent model, the base model, the underlying architecture itself, even where the model was trained and the hardware and the software that was actually used to train the model, the intended usage.

Part of the course introduce ths SPDX and Cyclone DX standard, those are the top two standards for software building materials. Many organizations are actually using both SPDX and Cyclone DX for distributing and consuming SBoMs.

Exist three ways to leveraging LLMs
- Train an LLM from scratch
- Fine-Tune an LLM
- Retrieval augmented generartion (RAG)

LLMs has an stack security layers that are compose for:
- API and interface layer
- Integration with other systems or platforms
- Model layer (model architecture, training algorithms)
- Optimization and training tools
- Data layer (training data, data processing tools)
- Hardware layer

Last but not least the course remark the importance and criticality of Monitoring and security including:

- Monitor not only for performance but for security
- Apply proper access control and authentication

These are security best practices. But in many cases, actually, they're not implemented in many organizations and in many solutions, especially as people are experimenting and then they put these solutions into production. 

In the words of "Omar Santos" whose the course speaker:

["After the experimentation phase, they will leave them in an insecure manner. Vector databases and search security, but specifically vector databases. Some of them do not supply a capability for encrypting data. So once again, some vector databases, even those that are either commercial or open source do not provide encryption. So you have to pay attention to that. And if you're working with a vendor, make sure that they actually are providing security elements like encryption and data protection for those databases. Regular audit and log as I mentioned to you login is extremely important. And whenever it comes to third party software security and supply chain security, definitely you have to pay attention to vulnerability management and patching those third party and open source libraries like LangChain, LlamaIndex, pgvector, ChromaDB, MongoDB, etc."]


25 August 2025
[J x 2] 

 
---

[← Volver al inicio]({{ "/" | relative_url }})
