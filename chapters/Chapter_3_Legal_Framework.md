
# CHAPTER 3: LEGAL FRAMEWORK AND LAW ENFORCEMENT ENGAGEMENT
## Prosecution Pathways for Cross-Border Mobile Cybercrime in Malaysia and Pakistan

---

**Document Classification:** Public Technical Report  
**Case Reference:** RAK/CYB/2026/001  
**Report Date:** June 2026  
**Version:** 1.0  

---

## EXECUTIVE SUMMARY

This chapter analyzes the legal frameworks applicable to the attack class documented in Chapter 1 — specifically, compromises involving device cloning, DSU/GSI multi-environment persistent infrastructure, baseband-level diagnostic exploitation, and cross-border command-and-control operations. The analysis focuses on two jurisdictions: **Malaysia** (the primary operational base of the attacker) and **Pakistan** (the victim's residence and the location of physical access exploitation events).

The legal landscape for prosecuting sophisticated mobile cybercrime is fragmented, with significant gaps between technical capability and legal framework. Malaysia's Computer Crimes Act 1997, Communications and Multimedia Act 1998, and the newly enacted Cyber Security Act 2024 provide a comprehensive statutory basis for prosecution, but face challenges in cross-border enforcement and the technical complexity of evidence presentation. Pakistan's Prevention of Electronic Crimes Act (PECA) 2016 offers direct applicability to the baseband and DSU/GSI findings, but suffers from low conviction rates and institutional capacity constraints.

This chapter provides:
1. Jurisdiction-specific legal framework analysis
2. Evidence requirements and admissibility standards
3. Chain of custody protocols for digital forensic evidence
4. Cross-border coordination mechanisms (INTERPOL, bilateral treaties, mutual legal assistance)
5. Practical recommendations for victims navigating law enforcement engagement

---

## 1. MALAYSIA: LEGAL FRAMEWORK ANALYSIS

### 1.1 Computer Crimes Act 1997 (CCA 1997)

The Computer Crimes Act 1997 is Malaysia's primary legislation addressing unauthorized access to computer systems, data, and communications. It was amended in 2023 to expand definitions and increase penalties.

**Section 3 — Unauthorized Access to Computer Material**
- Offense: Accessing computer material without authorization
- Penalty: Fine not exceeding MYR 50,000 or imprisonment not exceeding 5 years, or both
- **Applicability to Case RAK/CYB/2026/001:** The 9 device clones sharing the victim's IMEI and serial number constitute unauthorized access to the victim's Google Account device registry. The baseband QXDM diagnostic interfaces (Section 7 equivalent) provide unauthorized access to SMS, GPS, and voice call data.

**Section 4 — Access with Intent to Commit Offense**
- Offense: Accessing a computer with intent to commit a further offense (extortion, data theft, identity fraud)
- Penalty: Fine not exceeding MYR 150,000 or imprisonment not exceeding 10 years, or both
- **Applicability:** The ransom emails (7-8 instances, 6 drafted inside the victim's inbox) demonstrate intent to commit extortion. The 52,773 account access events in April 2026 indicate systematic data theft.

**Section 5 — Unauthorized Modification of Computer Material**
- Offense: Modifying computer material without authorization
- Penalty: Fine not exceeding MYR 100,000 or imprisonment not exceeding 10 years, or both
- **Applicability:** The DSU/GSI infrastructure modifications (3 bootable environments, Magisk root layer in boot partition ramdisk, hidden DSU Loader) constitute unauthorized modification. The rescue partition tampering (READ-WRITE mount state) and modem configuration modifications (QMCS, SPUNVM) are direct modifications.

**Section 6 — Wrongful Communication**
- Offense: Communicating information obtained through unauthorized access
- Penalty: Fine not exceeding MYR 70,000 or imprisonment not exceeding 7 years, or both
- **Applicability:** The attacker communicated stolen data (SMS, GPS, voice calls) via the QXDM diagnostic interfaces and exfiltrated Google Account data (Gmail, Drive, Calendar) through VPN infrastructure.

**Section 9 — Extra-Territorial Jurisdiction**
- Offense: Offenses committed outside Malaysia that produce effects within Malaysia
- Penalty: Same as domestic offenses
- **Applicability:** The attacker's operations from Malaysia affected the victim in Pakistan. Conversely, the attacker's physical access in Pakistan (December 2024) and the victim's presence in Malaysia (September 2025) create jurisdictional overlap.

### 1.2 Communications and Multimedia Act 1998 (CMA 1998)

The CMA 1998 addresses network-level offenses and provides additional prosecution pathways.

**Section 233 — Improper Use of Network Facilities**
- Offense: Using network facilities to transmit offensive, indecent, obscene, or menacing content
- Penalty: Fine not exceeding MYR 50,000 or imprisonment not exceeding 1 year, or both
- **Applicability:** The ransom emails and any threatening communications transmitted via the cloned devices or compromised accounts.

**Section 232 — Fraudulent Use of Network Services**
- Offense: Using network services fraudulently or without authorization
- Penalty: Fine not exceeding MYR 100,000 or imprisonment not exceeding 2 years, or both
- **Applicability:** The SIM cloning (Maxis Malaysian SIM) and device cloning (9 instances with shared IMEI) constitute fraudulent use of network services.

**Section 234 — Interception of Communications**
- Offense: Intercepting communications without authorization
- Penalty: Fine not exceeding MYR 100,000 or imprisonment not exceeding 2 years, or both
- **Applicability:** The QXDM baseband diagnostic interfaces provide real-time interception of SMS, voice calls, and GPS data — directly satisfying this provision.

**Section 235 — Damage to Network Facilities**
- Offense: Damaging or interfering with network facilities
- Penalty: Fine not exceeding MYR 150,000 or imprisonment not exceeding 3 years, or both
- **Applicability:** The tampered rescue partition and modem configuration modifications (QMCS, SPUNVM) interfere with the normal operation of network attachment and authentication procedures.

### 1.3 Penal Code (Malaysia)

**Section 383 — Extortion**
- Offense: Intentionally putting a person in fear of injury to person, reputation, or property, with intent to dishonestly induce delivery of property
- Penalty: Imprisonment not exceeding 10 years, or fine, or whipping, or any two of such punishments
- **Applicability:** The 7-8 ransom emails demanding 2,000 USDT to prevent release of stolen data constitute extortion.

**Section 384 — Punishment for Extortion**
- Penalty: Same as Section 383
- **Applicability:** The repeated nature of the ransom demands (October 2024, February-March 2026) indicates sustained extortionate conduct.

**Section 416 — Cheating by Personation**
- Offense: Cheating by pretending to be some other person, or by knowingly substituting one person for another
- Penalty: Imprisonment not exceeding 7 years, and fine
- **Applicability:** The device cloning (9 clones operating with the victim's IMEI and serial number) constitutes personation — the attacker impersonated the victim's device identity to access accounts and services.

**Section 420 — Cheating and Dishonest Inducement**
- Offense: Cheating and thereby dishonestly inducing delivery of property
- Penalty: Imprisonment not exceeding 10 years, and fine
- **Applicability:** The social engineering phase (dating app contact, manufactured intimacy) and subsequent technical exploitation constitute cheating with dishonest inducement.

### 1.4 Personal Data Protection Act 2010 (PDPA 2010)

**Section 130 — Data Breach Notification**
- Requirement: Data users must notify the Personal Data Protection Commissioner of any data breach
- Penalty for non-compliance: Fine not exceeding MYR 100,000 or imprisonment not exceeding 2 years, or both
- **Applicability:** If the attacker obtained personal data through the compromise and any entity (telecom, app provider) failed to notify, they may face liability. However, this is primarily a regulatory provision rather than a criminal one.

### 1.5 Cyber Security Act 2024 (New Legislation)

The Cyber Security Act 2024, effective 26 August 2024, represents Malaysia's most significant cybersecurity legislation update.

**Key Provisions:**
- Establishment of the National Cyber Security Committee (NCSC)
- Designation of National Critical Information Infrastructure (NCII) sectors
- Powers of the National Cyber Security Agency (NACSA) for threat monitoring and response
- Licensing requirements for cybersecurity service providers
- Mandatory reporting of cybersecurity incidents for NCII entities

**Applicability to Case RAK/CYB/2026/001:**
While the victim is not an NCII entity, the attacker's infrastructure (VPN services, cloud servers, telecom access) may intersect with NCII sectors. The Act provides a framework for coordinated national response to sophisticated cyber threats and may facilitate law enforcement coordination.

---

## 2. PAKISTAN: LEGAL FRAMEWORK ANALYSIS

### 2.1 Prevention of Electronic Crimes Act (PECA) 2016

PECA 2016 is Pakistan's primary cybercrime legislation, enacted to address the gaps in the Pakistan Penal Code 1860 for digital offenses.

**Section 3 — Unauthorized Access to Information System**
- Offense: Accessing an information system without authorization
- Penalty: Imprisonment not exceeding 3 years, or fine not exceeding PKR 1 million, or both
- **Applicability to Case RAK/CYB/2026/001:** The 9 device clones, baseband QXDM interfaces, and DSU/GSI infrastructure all constitute unauthorized access to the victim's information system (mobile device and associated accounts).

**Section 4 — Unauthorized Access to Critical Infrastructure**
- Offense: Accessing critical infrastructure information systems without authorization
- Penalty: Imprisonment not exceeding 7 years, or fine not exceeding PKR 5 million, or both
- **Applicability:** If the victim's device or accounts were connected to any critical infrastructure (government, telecom, financial), this enhanced penalty applies.

**Section 5 — Unauthorized Copying or Acquisition of Data**
- Offense: Copying or acquiring data without authorization
- Penalty: Imprisonment not exceeding 3 years, or fine not exceeding PKR 1 million, or both
- **Applicability:** The 52,773 account access events in April 2026, the 15,973 VPN events in February 2026, and the systematic exfiltration of Gmail, Drive, and Calendar data constitute unauthorized copying/acquisition.

**Section 6 — Unauthorized Interference with Information System**
- Offense: Interfering with the operation of an information system without authorization
- Penalty: Imprisonment not exceeding 7 years, or fine not exceeding PKR 5 million, or both
- **Applicability:** The tampered rescue partition (surviving factory reset), modified modem configuration (QMCS, SPUNVM), and Magisk root layer in the boot partition ramdisk all interfere with the normal operation of the information system.

**Section 7 — Unauthorized Interception of Data**
- Offense: Intercepting data in transmission without authorization
- Penalty: Imprisonment not exceeding 5 years, or fine not exceeding PKR 2 million, or both
- **Applicability:** This is the most directly applicable provision. The QXDM baseband diagnostic interfaces provide real-time interception of SMS messages, voice call audio, and GPS location data. The VPN infrastructure intercepts Google Account data in transmission. This provision directly addresses the core technical finding of Addendum C.

**Section 8 — Unauthorized Use of Identity Information**
- Offense: Using another person's identity information without authorization
- Penalty: Imprisonment not exceeding 3 years, or fine not exceeding PKR 1 million, or both
- **Applicability:** The device cloning (using the victim's IMEI, serial number, Android ID) and SIM cloning (using the victim's phone number and IMSI) constitute unauthorized use of identity information.

**Section 9 — Glorification of Offense**
- Offense: Glorifying, justifying, or encouraging commission of an offense
- Penalty: Imprisonment not exceeding 7 years, or fine not exceeding PKR 2 million, or both
- **Applicability:** If the attacker shared or publicized the compromise (e.g., distributing stolen data, boasting about the attack), this provision applies.

**Section 10 — Cyber Terrorism**
- Offense: Using an information system to commit terrorism (broadly defined)
- Penalty: Imprisonment not exceeding 14 years, or fine not exceeding PKR 5 million, or both
- **Applicability:** This is the most severe penalty under PECA. It requires proof that the attack was designed to create widespread fear, coerce the government or public, or advance a terrorist agenda. The sustained 600+ day campaign, cross-border coordination, and systematic surveillance may satisfy this definition if linked to a broader ideological or coercive purpose.

### 2.2 Pakistan Telecommunication Act 1996

**Section 24 — Interception of Communications**
- Offense: Intercepting communications without lawful authority
- Penalty: As prescribed by the Authority
- **Applicability:** The QXDM baseband interception of SMS and voice calls, and the VPN-based interception of Google Account data, constitute unauthorized interception under this Act.

**Section 54 — Fraudulent Use of Telecommunication System**
- Offense: Using a telecommunication system fraudulently or without authorization
- Penalty: Fine or imprisonment as prescribed
- **Applicability:** The SIM cloning and device cloning constitute fraudulent use of the telecommunication system.

### 2.3 Pakistan Penal Code 1860

**Section 378 — Theft**
- Offense: Dishonestly taking movable property out of possession of any person
- Penalty: Imprisonment not exceeding 3 years, or fine, or both
- **Applicability:** The data exfiltration (Gmail, Drive, Photos, Calendar) constitutes theft of intangible property (data).

**Section 383 — Extortion**
- Offense: Intentionally putting a person in fear of injury with intent to dishonestly induce delivery of property
- Penalty: Imprisonment not exceeding 10 years, or fine, or both
- **Applicability:** The ransom emails demanding 2,000 USDT constitute extortion.

**Section 419 — Cheating by Personation**
- Offense: Cheating by personation
- Penalty: Imprisonment not exceeding 7 years, or fine, or both
- **Applicability:** The device cloning (impersonating the victim's device) and SIM cloning (impersonating the victim's phone number) constitute cheating by personation.

**Section 420 — Cheating and Dishonest Inducement**
- Offense: Cheating and thereby dishonestly inducing delivery of property
- Penalty: Imprisonment not exceeding 7 years, or fine, or both
- **Applicability:** The social engineering and subsequent technical exploitation constitute cheating with dishonest inducement.

### 2.4 Electronic Transactions Ordinance 2002

**Section 38 — Unauthorized Access to Information System**
- Offense: Accessing an information system without authorization
- Penalty: Fine or imprisonment as prescribed
- **Applicability:** Overlaps with PECA Section 3 but provides an alternative prosecution pathway.

**Section 39 — Unauthorized Access to Protected System**
- Offense: Accessing a protected system without authorization
- Penalty: Enhanced penalties for protected systems
- **Applicability:** If the victim's device or accounts were classified as protected systems (e.g., government, financial, critical infrastructure).

**Section 40 — Unauthorized Modification of Information**
- Offense: Modifying information without authorization
- Penalty: Fine or imprisonment as prescribed
- **Applicability:** The DSU/GSI modifications, rescue partition tampering, and modem configuration modifications.

---

## 3. CROSS-BORDER COORDINATION MECHANISMS

### 3.1 The Jurisdictional Challenge

The attack class documented in Chapter 1 spans multiple jurisdictions:
- **Malaysia**: Attacker's operational base, location of device cloning (September 2025), location of DSU/GSI infrastructure configuration
- **Pakistan**: Victim's residence, location of physical access exploitation (December 2024), location of baseband forensic discovery
- **Sweden**: VPN infrastructure (Hern Labs AB, 15,973 access events)
- **Singapore**: Cloud server infrastructure (Alibaba Cloud, DigitalOcean)
- **Hong Kong**: Cloud server infrastructure (Alibaba Cloud)

This cross-border nature creates significant prosecutorial challenges:
- **Evidence collection**: Different legal standards for digital evidence admissibility
- **Extradition**: Malaysia and Pakistan have no bilateral extradition treaty
- **Mutual Legal Assistance (MLA)**: Slow process, often taking 6-18 months per request
- **Jurisdictional priority**: Which country prosecutes first? Which has stronger evidence?
- **Evidence sharing**: Privacy laws (EU GDPR for Sweden, PDPA for Malaysia) may limit data sharing

### 3.2 INTERPOL Coordination

INTERPOL provides several mechanisms for cross-border cybercrime coordination:

**Cyber Fusion Centre (Singapore)**
- Coordinates cybercrime intelligence sharing among member countries
- Provides technical analysis support for complex cases
- Issues Purple Notices (modus operandi) and Red Notices (wanted persons)

**Digital Forensics Laboratory (Lyon, France)**
- Provides expert forensic analysis for member countries
- Can validate forensic methodologies and evidence integrity
- Issues technical reports for court proceedings

**I-24/7 Secure Communications Network**
- Enables secure, real-time information exchange between national central bureaus (NCBs)
- Malaysia NCB: Royal Malaysia Police (PDRM)
- Pakistan NCB: Federal Investigation Agency (FIA)

**Applicability to Case RAK/CYB/2026/001:**
An INTERPOL Purple Notice could be issued documenting the attack methodology (DSU/GSI exploitation, baseband diagnostic abuse, device cloning) to alert other member countries. A Red Notice could be issued for the attacker if identity is confirmed and extradition is sought.

### 3.3 Bilateral Mutual Legal Assistance Treaties (MLAT)

Malaysia and Pakistan do not have a bilateral MLAT. However, both countries are parties to multilateral conventions that may facilitate cooperation:

**Council of Europe Convention on Cybercrime (Budapest Convention)**
- Malaysia: Not a party (but has observer status)
- Pakistan: Not a party
- **Implication:** Neither country can directly invoke Budapest Convention mechanisms for this case

**Commonwealth Scheme for Mutual Assistance in Criminal Matters**
- Both Malaysia and Pakistan are Commonwealth members
- Provides a framework for mutual assistance, but not automatic
- Requires diplomatic channel requests through Foreign Ministries

**United Nations Convention against Transnational Organized Crime (UNTOC)**
- Both countries are parties
- Article 18 provides for mutual legal assistance in criminal matters
- Can be invoked for cybercrime cases with transnational elements

**Practical Process:**
1. Victim reports to FIA Cyber Crime Wing (Pakistan) and PDRM Cyber Crime Unit (Malaysia)
2. FIA and PDRM conduct preliminary investigations independently
3. If cross-border evidence is needed, FIA sends MLAT request to Ministry of Foreign Affairs (Pakistan)
4. Ministry of Foreign Affairs forwards request to Malaysian High Commission in Islamabad
5. Malaysian High Commission forwards to Ministry of Foreign Affairs (Malaysia)
6. Ministry of Foreign Affairs forwards to Attorney General's Chambers (Malaysia)
7. Attorney General's Chambers forwards to PDRM for execution
8. PDRM collects evidence and returns through same chain

**Timeline:** 6-18 months for each request. Multiple requests may be needed (VPN logs, cloud server data, telecom records).

### 3.4 Direct Law Enforcement Cooperation

In practice, direct cooperation between FIA Cyber Crime Wing and PDRM Cyber Crime Unit may be faster than formal MLAT:

**FIA Cyber Crime Wing (CCW)**
- Primary investigative body for cybercrime in Pakistan
- National Response Centre for Cyber Crime (NR3C) provides technical support
- Jurisdiction: Federal level, cross-border coordination
- Contact: Director, FIA Cyber Crime Wing, Islamabad

**PDRM Cyber Crime Unit**
- Part of the Commercial Crime Investigation Department (CCID)
- Handles cybercrime investigations under CCA 1997 and CMA 1998
- Contact: Head of Cyber Crime Unit, CCID, Kuala Lumpur

**Recommended Approach:**
1. Victim files simultaneous complaints in BOTH jurisdictions
2. FIA CCW and PDRM CCID establish direct contact through INTERPOL NCBs
3. Joint investigation team (JIT) formed with representatives from both agencies
4. Evidence sharing through INTERPOL I-24/7 secure channel
5. Parallel prosecution in both jurisdictions (if extradition is not feasible)

---

## 4. EVIDENCE REQUIREMENTS AND ADMISSIBILITY

### 4.1 Malaysian Standards

**Evidence Admissibility (Evidence Act 1950, as amended)**
- Section 90A: Admissibility of computer-generated documents
- Requirements: Document must be produced by computer in ordinary course of activity; computer must have been operating properly
- **Challenge for DSU/GSI evidence:** Computer-generated evidence from a compromised device may be challenged as unreliable. Independent forensic verification (Cellebrite, XRY) is essential.

**Chain of Custody**
- Every handler from seizure to court presentation must be documented
- Breaks in chain may render evidence inadmissible
- Over 90% of UK court cases involving digital evidence hinge on preservation and presentation quality
- **Critical for this case:** The baseband forensic analysis (AIDA64, QPST) and DSU/GSI discovery must be conducted by certified forensic examiners with documented methodology

**Expert Witness Requirements**
- Expert must be qualified in the relevant field (digital forensics, mobile security, network analysis)
- Expert must provide independent, unbiased opinion
- Expert must be able to explain technical concepts in accessible language
- Expert must be prepared for cross-examination on methodology, limitations, and alternative explanations

### 4.2 Pakistani Standards

**Evidence Admissibility (Qanun-e-Shahadat Order 1984)**
- Article 164: Admissibility of documentary evidence
- Requirements: Document must be genuine, relevant, and properly authenticated
- **Challenge for digital evidence:** Pakistani courts have historically been conservative in admitting digital evidence. Forensic certification and expert testimony are essential.

**Chain of Custody (Criminal Procedure Code 1898)**
- Section 103: Search and seizure procedures
- Requirements: Seizure must be witnessed, documented, and properly stored
- **Critical for this case:** The device seizure in Pakistan (if applicable) or Malaysia must follow strict procedures

**PECA 2016 Specific Provisions**
- Section 29: Presumption of guilt for unauthorized access (if device is found in possession of accused)
- Section 30: Presumption of authenticity for electronic records (if properly certified)
- **Applicability:** If the attacker is found in possession of cloned devices or compromised accounts, presumption of guilt may apply.

### 4.3 Cross-Border Evidence Challenges

**VPN Log Evidence (Sweden — Hern Labs AB)**
- EU GDPR may limit data sharing without Swedish court order
- Swedish Penal Code Chapter 7 (Brottsbalken) provides for data preservation orders
- **Process:** Malaysian or Pakistani prosecutor must request Swedish court to issue preservation order; then request data disclosure through MLAT

**Cloud Server Evidence (Singapore — Alibaba Cloud, DigitalOcean)**
- Singapore Personal Data Protection Act 2012 (PDPA) governs data sharing
- Singapore Computer Misuse Act 1993 provides for data preservation
- **Process:** Direct law enforcement cooperation between PDRM/FIA and Singapore Police Force (Cybercrime Command) may be faster than MLAT

**Google Takeout Evidence**
- Google will comply with valid legal requests (subpoena, court order, warrant)
- Process: Law enforcement agency submits request through Google Law Enforcement Request System (LERS)
- Timeline: 10-30 days for standard requests; emergency requests (imminent harm) may be faster
- **Critical:** The victim's own Google Takeout export is admissible as personal record, but independent verification through Google LERS is stronger evidence

---

## 5. CHAIN OF CUSTODY PROTOCOL

### 5.1 Digital Forensic Evidence Preservation

The chain of custody for digital evidence is the most common point of failure in cybercrime prosecution. Over 90% of UK court cases involving digital evidence hinge on preservation and presentation quality. Every handler from patrol officer to forensic examiner can be subpoenaed and held accountable for evidence handling.

**Phase 1: Device Seizure**
- Photograph device in situ (serial, IMEI, physical state)
- Record exact time, date, location of seizure
- Document who seized, who witnessed, environmental conditions
- Do NOT power on device — maintain power state as found
- If device is ON, enable airplane mode immediately (if safe)
- If device is OFF, do NOT power on

**Phase 2: Faraday Bag Isolation**
- Place device in RF-shielded Faraday bag immediately
- Seal bag with tamper-evident tape
- Label with case number, date, time, handler initials
- Maintain bag sealed until forensic examination
- Store in secure, climate-controlled environment
- Log every access to storage location

**Phase 3: Forensic Imaging**
- Use write blockers for ALL storage media access
- Create bit-by-bit forensic duplicate (dd, FTK Imager, Cellebrite)
- Calculate and record hash (MD5, SHA-1, SHA-256) of original
- Verify hash match between original and duplicate
- Work ONLY on duplicate — never on original
- Document imaging tool version, settings, examiner credentials

**Phase 4: Chain of Custody Log**
- Maintain chronological log of ALL evidence handling
- Record: who, what, when, where, why for each access
- Use standardized evidence handling form
- Require signature for every transfer of custody
- Include digital signatures and timestamps where possible
- Blockchain-based custody logging (emerging best practice)

**Phase 5: Expert Witness Preparation**
- Prepare clear, non-technical summary for jury/judge
- Document examiner qualifications and certifications
- Conduct mock cross-examination with legal counsel
- Anticipate challenges: chain of custody, tool reliability, alternative explanations, examiner bias
- Prepare visual aids: timelines, diagrams, screenshots
- Ensure all findings are reproducible by independent examiner

**Phase 6: Court Presentation**
- Present evidence in chronological order
- Use visualizations: attack timeline, infrastructure map, clone registry, access volume charts
- Explain technical concepts in accessible language
- Address defense challenges directly and transparently
- Acknowledge limitations of forensic analysis
- Maintain professional demeanor under cross-examination

### 5.2 Specific Considerations for This Case

**Baseband Evidence (QXDM, QPST)**
- Baseband analysis requires specialized tools (QPST, QFIL) not commonly used in standard mobile forensics
- Examiner must demonstrate expertise in Qualcomm baseband architecture
- Evidence must be presented with clear explanation of QXDM capabilities and implications
- Defense may challenge: "How do we know these interfaces were actively used, not just present?"
- **Response:** Document active session logs, network traffic correlation, or behavioral evidence (SMS interception, GPS tracking)

**DSU/GSI Evidence**
- DSU/GSI analysis is cutting-edge; few forensic examiners have experience
- Examiner must demonstrate understanding of Android Dynamic System Updates, Project Treble, and GSI builds
- Evidence must be presented with clear explanation of multi-environment architecture
- Defense may challenge: "How do we know these environments were actually used, not just present?"
- **Response:** Document boot logs, network traffic from GSI environments, or account access patterns consistent with GSI operation

**Remote Emulator Architecture**
- This is the most complex evidence to present
- Requires network traffic analysis, VPN log correlation, and cloud server forensics
- Examiner must demonstrate understanding of remote Android environments, VPN tunneling, and identity relay
- Defense may challenge: "How do we know the device was relaying to a remote server, not just running a local emulator?"
- **Response:** Document network traffic patterns, VPN endpoint correlation, and behavioral evidence (device in Pakistan while account accessed from Malaysia)

---

## 6. PRACTICAL RECOMMENDATIONS FOR VICTIMS

### 6.1 Immediate Reporting

**Malaysia:**
- Report to PDRM Cyber Crime Unit (CCID) immediately
- File report at nearest police station with cyber crime capability
- Provide: device, Google Takeout data, network logs, timeline of events
- Request: case number, investigating officer contact, estimated timeline

**Pakistan:**
- Report to FIA Cyber Crime Wing (CCW) immediately
- File complaint online at nr3c.gov.pk or in person at FIA headquarters
- Provide: device, Google Takeout data, network logs, timeline of events
- Request: complaint number, investigating officer contact, estimated timeline

**Both Jurisdictions:**
- File SIMULTANEOUS complaints in both countries
- Request that both agencies coordinate through INTERPOL
- Document ALL interactions with law enforcement (dates, names, case numbers)
- Follow up weekly if no response within 14 days

### 6.2 Evidence Preparation

**Organize Evidence Chronologically**
- Create a master timeline of ALL events (October 2024 – June 2026)
- Include: dates, times, locations, devices, accounts, communications
- Cross-reference with Google Takeout data, network logs, CCTV footage

**Prepare Technical Evidence**
- Export Google Takeout (ALL data categories)
- Save network logs (router, ISP, VPN)
- Preserve CCTV footage (with timestamps, before overwrite)
- Document device state (photos, AIDA64 exports, QPST logs)

**Prepare Witness Evidence**
- Identify witnesses who observed attacker's behavior
- Document witness statements with dates, locations, specific observations
- Include: CCTV time gap observations, audio anomalies, physical access incidents

**Prepare Financial Evidence**
- Document ransom demands (screenshots, email headers, blockchain transactions)
- Document financial losses (device replacement, account recovery, legal fees)
- Document emotional/psychological impact (counseling records, medical reports)

### 6.3 Legal Representation

**Malaysia:**
- Engage criminal lawyer with cybercrime experience
- Consider: Messrs. Shook Lin & Bok, Messrs. Zaid Ibrahim & Co., Messrs. Lee Hishammuddin Allen & Gledhill
- Request legal aid if eligible (Bantuan Guaman)

**Pakistan:**
- Engage criminal lawyer with PECA experience
- Consider: High Court advocates with cybercrime specialization
- Request legal aid if eligible (Provincial Legal Aid Authority)

**Both Jurisdictions:**
- Lawyer should have experience with digital evidence and expert witness coordination
- Lawyer should be prepared for cross-border coordination challenges
- Consider engaging a digital forensics expert as consultant (not just witness)

### 6.4 Media and Public Attention

**Considerations:**
- Public attention can pressure law enforcement to prioritize the case
- Public attention can also alert the attacker, who may destroy evidence or flee
- Media coverage may compromise the victim's privacy and safety
- Social media posts may be used as evidence (or challenged by defense)

**Recommendations:**
- Consult legal counsel before any media engagement
- Use anonymized technical reports (like this document) for awareness without personal exposure
- Coordinate with law enforcement on timing of public disclosure
- Consider victim protection measures (relocation, security detail) if attacker is identified and at large

---

## 7. CONCLUSION

The legal frameworks in both Malaysia and Pakistan provide comprehensive statutory bases for prosecuting the attack class documented in Chapter 1. Malaysia's Computer Crimes Act 1997 (as amended 2023), Communications and Multimedia Act 1998, and Cyber Security Act 2024 offer strong penalties and extra-territorial jurisdiction. Pakistan's PECA 2016 provides direct applicability to the baseband and DSU/GSI findings, with Section 7 (Unauthorized Interception) being the most directly applicable provision.

However, the cross-border nature of the case creates significant practical challenges. The lack of a bilateral extradition treaty between Malaysia and Pakistan, the slow MLAT process (6-18 months per request), and the technical complexity of evidence presentation all complicate prosecution.

The key success factors are:
1. **Simultaneous reporting** in both jurisdictions with explicit request for INTERPOL coordination
2. **Rigorous evidence preservation** following chain of custody protocols
3. **Expert forensic examination** by certified examiners with baseband and DSU/GSI expertise
4. **Expert witness preparation** for accessible, credible court presentation
5. **Persistent follow-up** with law enforcement to maintain case priority
6. **Legal representation** with cybercrime experience and cross-border coordination capability

The case is prosecutable. The evidence is strong. The legal frameworks are adequate. The challenge is execution — converting technical findings into legal convictions across borders and jurisdictions.

---

**Next Chapter:** Chapter 4 — Advanced Forensic Techniques for Mobile Device Investigation
