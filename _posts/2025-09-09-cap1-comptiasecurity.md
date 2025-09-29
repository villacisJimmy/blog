 ---
layout: post
title: "CompTIA Security+ Certification Cap-1"
date: 2025-09-25
categories: [blog]
 ---
 
# Title  
CompTIA Security+ Certification Cap-1


Confidentiality
  -> Unauthorized individuals are not able to gain access to sensitive information
  -> Security Controls 
    -> Firewalls
    -> ACL
    -> Encryption
  -> Unauthorized disclosure of sensitive information

Integrity
  -> Ensures that information on systems is ready to meet the needs of legitimate users at the time those users request it.
    -> Fault tolerance 
    -> Clustering 
    -> Backups
  -> Ensures that legitimate users may gain access as needed

* Cybersecurity Analysts often refer to these three goals, known as the CIA triad
-> They often characterize risks, attacks, and security controls as meeting one or more of the three CIA triad goals when describing them.

Non repudiation
  -> It's also an important goal of some cybersecurity controls.
    -> Someone who performed some action, such as sending a message, cannot later deny having taken that action
      -> Digital Signature

Data Breach Risks
  -> Security incidents occur when an organization experiences a breach of confidentiality, integrity, and/or availability.

Security Professionals are responsible for understanding these risks and implementing controls designed to manage those risks to an acceptable level
  -> First, understand the effects that a breach might have on your organization and the impact it might have on an ongoing basis.

The DAD triad
  -> Explains the three key threats maps directly to one of the main goals of cybersecurity

Disclosure 
  -> The exposure of sensitive information to unauthorized individuals, otherwise known as "data loss"
  -> Violation of confidentiality
  -> Attackers who gain access to sensitive information and remove it from the organization are said to be performing data exfiltration
  -> Also occurs accidentally 

Alteration
  -> The unauthorized modification of information and is a violation of integrity
  -> Modify records contained in a system
  -> Natural activity, such as a power surge, causing a "bit flip" that modifies stored data
  -> Accidental alteration (typo or other unintentional activity)

Denial
  -> The disruption of an authorized user's legitimate access to information
  -> Violate the principle of "availability"
  -> DDoS
  -> Accidental activity (failure of a critical server)

* CIA and DAD -> Useful for cybersecurity planning and risk analysis(guidance)

Example: If you're asked to assess the threats to your organization's website, you may apply the DAD triad in your analysis
  -> Does the website contain sensitive information that would damage the organization if disclosed to unauthorized individuals?
  -> If an attacker were able to modify information contained on the website, would this unauthorized alteration cause financial, reputational, or operational damage to the organisation?
  -> Does the website perform mission-critical activities that could damage the business significantly if an attacker were able to disrupt the site?

Breach Impact
  -> The impact, depending on the nature of the incident and the type of organization affected
  -> We can categorize the potential impact of a security incident in (financial, reputational, strategic, operational, and compliance)

Financial Risk 
  -> Monetary damage as a result of a data breach
  -> Direct and indirect

Reputational Risk
  -> Negative publicity surrounding a security breach causes the loss of goodwill among customers, employees, suppliers, and other stakeholders
  -> Difficult to quantify

Identify Theft
  -> When a security breach strikes an organization, the effects extend beyond the walls of  the breached organization. The most common impact is the risk of identity theft posed by the exposure of personally identifiable information (PII) to unscrupulous individuals.
    -> Organization should take special care to identify, inventory, and protect PII elements, especially those that are prone to use in identity theft crimes
      -> Social Security Number
      -> Bank Account
      -> Credit Card Information
      -> Driver's License Numbers
      -> Passport Data

Strategic Risk
  -> The risk that an organization will become less effective in meeting its major goals and objectives as a result of the breach

Operational Risk
  -> Risk to the organization's ability to carry out its day-to-day functions 
  -> May slow down business processes, delay delivery of customer orders, or require the implementation of time-consuming manual workaround to normally automated practices
  -> Operational and Strategic risk are closely related (difficult to distinguish between them)
  -> If a risk threatens the very existence of an organization or the ability of the organization to execute its business plans (strategic risk)
  -> If the risk only causes inefficiency  and delay within the organization, it fits better into the (operational risk) category

Compliance Risk
  -> Occurs when a security breach causes an organization to run afoul of legal or regulatory requirements
    -> Health Insurance Portability and Accountability Act (HIPAA)
      -> Requires that health-care providers and other covered entities protect the confidentiality, integrity, and availability of protected health information (PHI)
  -> Organizations face many different types of compliance risk in today's regulatory landscape 
  -> The nature of those risks depends on the jurisdictions where the organization operates, the industry that the organization functions within, and the types of data that the organization handles

* A risk crosses multiple categories

Implementing Security Controls 
  -> As an organization analyzes its risk environment, technical and business leaders determine the level of protection required to preserve the confidentiality, integrity, and availability of their information and systems.
  -> Control Objectives (What the organization wishes to achieve)
    -> These control objectives are statements of a desired security state, but they do not, by themselves, actually carry out security activities.
    -> Security controls are specific measures that fulfill the security objectives of an organization

Gap Analysis
  -> Cybersecurity professionals are responsible for conducting gap analyses to evaluate security controls
    -> During a gap analysis, the professional reviews the control objectives for a particular organization, system, or service and then examines the controls designed to achieve those objectives
      -> If there are any cases where the controls do not meet the control objective (that’s a gap)
        -> Should be treated as potential risks and remediated as time and resources permit.

Security Control Categories
  -> They are categorized based on their mechanism of action
    -> The way that they achieve their objectives
      -> There are four categories of security controls 
        -> Technical controls (enforce confidentiality, integrity, and availability in the digital space)
          -> Firewall rules
          -> ACL
          -> IPS
          -> Encryption
        -> Operational Controls (Processes that we put in place to manage technology securely)
          -> User access reviews
          -> Log monitoring
          -> Vulnerability management
        -> Managerial control (Procedural mechanisms that focus on the mechanics of the risk management process)
          -> Periodic risk assessments
          -> Security planning exercises 
        -> The incorporation of security into the organization's change management, service acquisition, and project practices
        -> Physical Controls (Security controls that impact the physical world)
          -> Fences
          -> Perimeter lighting
          -> Locks
          -> Fire suppression systems
          -> Burglar alarms
  -> Organisations should select a set of security controls that meets their control objectives based on the criteria and parameters that they either select for their environment or have imposed on them by outside regulators

Security Control Types 
  -> Based on their desired effect
    -> Preventive controls (intend to stop a security issue before it occurs)
      -> Firewall
      -> Encryption
    -> Deterrent controls (Seek to prevent an attacker from attempting to violate security policies)
      -> Vicious guard dogs
      -> Barbed wire fences
    -> Detective controls (identify security events that have already occurred)
      -> IDS
    -> Corrective Controls (remediate security issues that have already occurred)
      -> Restoring backups after a ransomware attack
    -> Compensating controls (controls designed to mitigate the risk associated with exceptions made to a security policy)
    -> Directive controls (inform employees and others what they should do to achieve security objectives)
      -> Policies and Procedures

Compensating Controls
  -> Payment Card Industry Data Security Standard (PCI DSS)
    -> One of the most formal compensating control processes in use today
  -> It sets out three criteria that must be met for a compensating control to be satisfactory
    -> The control must meet the intent and rigor of the original requirement
    -> The control must provide a similar level of defense as the original requirement, such that the compensating control sufficiently offsets the risk that the original PCI DSS requirement was designed to defend against
    -> The control must be "above and beyond" other PCI DSS requirements
  -> Compensating control finds alternative means to achieve an objective when the organization cannot meet the original control requirement
    -> The use of compensating controls is a common strategy in many different organizations
    -> Compensating controls balance the fact that it simply isn’t possible to implement every required security control in every circumstance, with the desire to manage risk to the greatest feasible degree
  
  * In many cases, organizations adopt compensating controls to address a temporary exception to a security requirement
    -> The organization should develop remediation plans designed to bring the organization back into compliance with the literal meaning and intent of the original control

Data Protection
  -> Protection of sensitive data
  -> We serve as stewards and guardians, protecting the confidentiality, integrity, and availability of the sensitive data
  -> 3 states where data might exist
    -> Data at rest (stored data that resides on hard drives, tapes, in the cloud, or other storage media)
      -> Insiders or external attackers who gain access to systems
    -> Data in transit (data that is in motion/transit over a network)
      -> When data travels on an untrusted network, it's open to eavesdropping attacks by anyone with access to those networks
    -> Data in use (it's actively in use by a computer system)
      -> Data stored in memory while processing takes place

* We can use different security controls to safeguard data in all of those states

Data encryption
  -> Mathematical algorithms to protect information from prying eyes, both while it is in transit over a network and while it resides on systems

Data Loss Prevention (DLP)
  -> Help organizations enforce information handling policies and procedures to prevent data loss and theft
    -> Sensitive information that is insecure in systems 
    -> Monitor network traffic
  -> They can block the transmission before damage is done and alert administrators to the attempted breach

DLP works in two different environments 
  1. Agent-based DLP
  2. Agentless (network-based) DLP

1) Uses software agents installed on systems that search those systems for the presence of sensitive information
   -> Social Security Number
   -> Credit and Number
   -> Etc.

   -> Remove it or secure it with encryption
     -> Can also monitor system configuration and user actions, blocking undesirable actions

Ex: Host-based DLP to block users from accessing USB-based removable media devices

2) Dedicated devices that sit on the network and monitor outbound network traffic, watching for any transmissions that contain unencrypted sensitive information
   -> Block those transmissions

DLP systems may simply block traffic that violates the organization's policy or may automatically apply encryption to the content that is commonly used, with a focus on email
DLP systems also have 2 mechanisms of action
  -> Pattern matching (where they watch for the telltale signs of sensitive information)
  -> Watermarking (electronic tags to sensitive documents, and then DLP systems can monitor systems and networks for unencrypted content containing those tags)
  -> Watermarking is also commonly used in digital rights management (DRM) solutions that enforce copyright and data ownership restrictions

Data Minimization
  -> Reduce risk by reducing the amount of sensitive information
  -> The best way to achieve data minimization is to simply destroy data when it is no longer necessary to meet our original business purpose
  -> We can transform it with a deidentification process that removes the ability to link data back, reducing its sensitivity 
    -> An alternative to deidentifying data is transforming it into a format where the original information can't be retrieved (Data Obfuscation)
      -> Hashing (transform a value into a corresponding hash value)
      -> Tokenization (Replaces sensitive values with a unique identifier using a lookup table)
      -> Masking partially (redacts sensitive information by replacing some or all sensitive fields with blank characters)

* Against hash, it's possible to conduct a rainbow table attack

Access Restrictions
  -> Security measures that limit the ability of individuals or systems to access sensitive information or resources
    -> Geographic restrictions (based on the physical location of the user or system)
    -> Permission Restrictions (based on the user's role or level of authorization)

* Organizations can ensure that sensitive information and resources are only accessible to authorized individuals and systems

Segmentation and Insolation
  -> Limit access to sensitive systems based on their network location
  -> Segmentation has strict restrictions on its ability to communicate with systems on other networks
  -> Isolation completely cuts a system off from access to or from the outside network



25 September 2025
[J x 2] 

 
---

[← Volver al inicio]({{ "/" | relative_url }})
