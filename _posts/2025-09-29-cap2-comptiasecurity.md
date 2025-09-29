---
layout: post
title: "CompTIA Security+ Certification Cap-2"
date: 2025-09-29
categories: [blog]
---
 
# Title  
CompTIA Security+ Certification Cap-2

Cybersecurity Threats Classification  
-> Internal/External
-> Level of Sophistication/Capability - unsophisticated/unskilled to APT
-> Resources/Funding  
-> Intent/Motivation  

Three types of hats to distinguish hackers
-> White
-> Black
-> Gray

-> Unskilled attackers (script kiddies) -- no specific reason
-> Hacktivists -- disagree with company policies/politics
-> Organized crime -- money
-> APT
  -> Nation-state -- political or economic motivation
  -> Shadow IT

Cybercrime categories by EUROPOL
-> cyber-dependent crime
-> Child sexual abuse  
-> Online fraud
-> Dark web activity
-> Cross-cutting crime factors  

Zero-day attacks  
-> Vulnerabilities that are not known to other attackers or cybersecurity teams  
-> Dangerous because they are unknown to product vendors  

Insider Attack
-> Individuals with authorized access to information and systems use that access to wage an attack against the organization
  -> Shadow IT poses a risk to the organization because it puts sensitive information in the hands of vendors outside of the organization's control

Competitors
  -> Corporate espionage (business advantage)

Attacker Motivation
  -> Data exfiltration (sensitive or proprietary information)
  -> Espionage (steal secret info)
  -> Service disruption (take down or interrupt critical systems or networks)
  -> Blackmail (extort money or other concessions)
  -> Financial gain (make money through theft or fraud)
  -> Philosophical/political belief (ideological or political reasons)
  -> Ethical attacks (expose vulnerabilities and improve security)
  -> Revenge (embarrassing them as a form of retribution)
  -> Disruption/chaos
  -> War (disrupt military operations)

Threat vectors and attack surfaces
-> Discover attack surface (system, application, service)
-> Obtain access by exploiting a vulnerability using a "threat vector"

*Reduce the size and complexity of the attack surface  
  -> Effective security measures  
  -> Risk mitigation strategies

Message-Based threat vector  
  -> Email $\to$ phishing messages
  -> SMS (short message service)
  -> Instant messaging (IM)
  -> Voice calls $\to$ vishing
  -> Social media (harvest information)

Wired Networks
  -> Physically entering the organization's facilities
    -> Connect to unsecured network jacks on the wall
    -> Find an unsecured computer terminal, network device, etc.

Wireless networks
  -> Easier path onto an organization's network

Systems
  -> Individual systems may also serve as threat vectors depending on how they are configured and the software installed on them

Files and images
  -> Embedded malicious code (malware infection)

Removable devices
  -> USB drives, to spread malware

Cloud
  -> Scan cloud services for files with improper access controls
    -> An important component of their security program

Supply Chain
  -> Hardware providers, software providers, and service providers
  -> Indirect mechanism

* Attackers who infiltrate managed service providers (MSPs) may be able to use their access to the MSP network to leverage access that the MSP has to its customers' systems and networks

Threat Data and Intelligence
  -> It's the set of activities and resources available to cybersecurity professionals seeking to learn about changes in the threat environment
    -> Threat intelligence program is a crucial part of an organization
  -> OSINT
  -> Commercial services that provide proprietary or closed-source intelligence information
  -> Threat Feeds
    -> IPs
    -> Hostnames/domains
    -> Email addresses
    -> URLs
    -> File hashes
    -> File paths
    -> CVEs
    -> Databases (critical)

* IOCs: these are the telltale signs that an attack has taken place and may include file signatures, log patterns, and other evidence
    -> Files and code repositories (Threat Intelligence Information)

Open Source Intelligence
    -> Publicly available sources
    -> The challenge is often around deciding what threat intelligence sources to use, ensuring that they are reliable and up-to-date, and leveraging them well

Dark Web
    -> It's a network run over a standard internet connection, but using multiple layers of encryption to provide anonymous communication

Proprietary and closed-source intelligence
    -> Commercial security vendors, government organizations, and other security-centric organizations also create and make their own information gathering and research, and they may use custom tools, analysis models, or other proprietary methods to gather, curate, and maintain their threat feeds
    -> The organization may want to keep their data secret, sell it, or license it, and their methods and sources are their trade secrets, or they may not want threat actors knowing about the data that they are gathering
    -> Identifying relevant threats and then ensuring that they are both well defined and applied appropriately for your organization can require massive amounts of effort

When a threat feed fails  
  -> It's critical that you have reliable, up-to-date feeds to avoid a critical situation
    -> You may want to have multiple feeds that you can check against each other

Threat Maps
  -> Provide a geographic view of threat intelligence  
  -> Organizations may also use threat mapping information to gain insight into the sources of attacks aimed directly at their networks

* Attackers often relay their attacks through cloud services and other compromised networks, hiding their true geographic location from threat analysis tools

Assessing Threat Intelligence
  -> Regardless of the source of your threat intelligence information, you need to assess it
    1) Is it timely?
      -> A feed that is operating on delay can cause you to miss a threat, or to react after the threat is no longer relevant
    2) Is the information accurate?
      -> Can you rely on what it says, and how likely is it that the assessment is valid? Does it rely on a single source or multiple sources? How often are those sources correct?
    3) Is the information relevant?
      -> If it describes the wrong platform, software, or reason for the organization to be targeted, the data may be very timely, very accurate, and completely irrelevant to your organization
  -> One way to summarize the threat intelligence assessment data is via a confidence score
    -> Filter and use threat intelligence based on how much trust they can give it
    -> Doesn't mean that lower confidence information isn’t useful
    -> A lot of threat intelligence starts with a lower confidence score, and the score increases as the information solidifies and as additional sources of information confirm it or are able to do a full analysis

Assessing the confidence level of your intelligence
  -> One approach uses six levels of confidence
    -> Confirmed (90-100) uses independent sources or direct analysis to prove that the threat is real
    -> Probable (70-89) relies on logical inference but does not directly confirm the threat
    -> Possible (50-69) is issued when some information agrees with the analysis, but the assessment is not confirmed
    -> Doubtful (30-49) is assigned when the assessment is possible, but not the most likely option
      -> Cannot be proven or disproven by the available information
    -> Improbable (2-29): the assessment is possible, but is not the most logical option
      -> Refuted by other available information
    -> Discredited (1) is used when the assessment has been confirmed to be inaccurate or incorrect

* Your organization may use a different scale
    -> 1-5, 1-10, and High/Medium/Low

Threat indicator management and exchange
  -> Managing threat information at any scale requires standardization and tooling to allow the threat information to be processed and used in automated ways
  -> Indicators management can be much easier with a defined set of terms
    -> STIX
    -> Open IOC
  -> Structured Threat Information eXpression (STIX) is an XML language
    -> Attack patterns
    -> Identities
    -> Malware  
    -> Threat actors
  -> These objects are then related to each other by one of two STIX Relation Objects (either as a relationship or as a sighting)

* Many organizations leverage multiple threat feeds to get the most up-to-date information
  -> Threat feed combinations can also be challenging since the feeds may not use the same format, classification model, or other elements

STIX has been handed off to the Organization for the Advancement of Structured Information Standards (OASIS)
  -> A companion to STIX is the Trusted Automated eXchange of Intelligence Information (TAXII) protocol

Information Sharing Organizations
  -> Threat intelligence vendors and resources, threat intelligence communities have been created to share threat information
    -> Information Sharing and Analysis Centers (ISACs) help infrastructure owners and operators share threat information and provide tools and assistance to their members
    -> ISACs operate on a trust model, allowing in-depth sharing of threat information for both physical and cyber threats

Conducting your own research
  -> You should continue to conduct your own research into emerging cybersecurity threats
    -> Sources you might consult
      -> Vendor security information websites
      -> Vulnerability and threat feeds from vendors, government agencies, and private organizations
      -> Academic journals and technical publications such as RFC documents
      -> Professional conferences and local industry group meetings  
      -> Social media accounts of prominent security professionals

* Keep a particular eye out for information on adversary tactics, techniques, and procedures (TTPs)


 
29 September 2025
[J x 2] 

 
[← Volver al inicio]({{ "/" | relative_url }})
