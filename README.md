# RAK-CYB-2026-001: Anatomy of a Sophisticated Android RAT Campaign

> **Technical Case Study in Multi-Vector Mobile Compromise with DSU/GSI Infrastructure and Baseband Forensic Analysis**

[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
[![Security Research](https://img.shields.io/badge/Type-Security%20Research-red.svg)]()
[![Android](https://img.shields.io/badge/Platform-Android-green.svg)]()
[![Forensics](https://img.shields.io/badge/Domain-Mobile%20Forensics-blue.svg)]()

---

## ⚠️ CRITICAL SECURITY ADVISORY

This repository documents a **600+ day sustained attack campaign** against a single individual's Android mobile ecosystem. The attack class involves:

- **9 unauthorized device clones** with shared IMEI/serial numbers
- **3 independently bootable OS environments** (DSU/GSI multi-environment infrastructure)
- **Baseband-level diagnostic exploitation** (Qualcomm QXDM interfaces below Android OS)
- **Remote Emulator Architecture** (device acts as relay for remotely hosted Android 16 environment)
- **Cross-border command-and-control** via commercial VPN chains and cloud servers

**Standard defensive measures (factory reset, password changes, app removal) are INEFFECTIVE against this attack class.** This repository provides the forensic evidence, legal framework analysis, and advanced remediation protocols required to detect and respond to similar compromises.

---

## 📋 Table of Contents

| Chapter | Title | Description | Word Count |
|---------|-------|-------------|------------|
| [Chapter 1](chapters/Chapter_1_Anatomy_of_Android_RAT.md) | Anatomy of a Sophisticated Android RAT Campaign | Technical case study: 600+ day attack timeline, device cloning, DSU/GSI infrastructure, baseband exploitation | ~8,000 |
| [Chapter 2](chapters/Chapter_2_Defensive_Countermeasures.md) | Defensive Countermeasures and Recovery Protocols | Post-compromise remediation: device quarantine, account isolation, network sanitization, ongoing monitoring | ~4,200 |
| [Chapter 3](chapters/Chapter_3_Legal_Framework.md) | Legal Framework and Law Enforcement Engagement | Malaysia vs Pakistan prosecution pathways, cross-border coordination, evidence admissibility, chain of custody | ~5,800 |
| [Chapter 4](chapters/Chapter_4_Advanced_Forensics.md) | Advanced Forensic Techniques for Mobile Device Investigation | DSU/GSI forensic analysis, baseband dump procedures, QXDM detection, tool comparison matrix | ~5,600 |
| [Expert Review](chapters/Expert_Review_Kimi_K2.6.md) | Expert Technical Review by Kimi K2.6 | Independent AI assessment: confidence levels, verified claims, questionable claims, recommendations | ~2,400 |

**Total Package:** ~26,000 words | 20 visualizations | 9+ credible sources | 4 jurisdictions

---

## 🎯 Key Findings (Executive Summary)

### Attack Timeline
- **Duration:** October 2024 – June 2026 (600+ days)
- **Geographic Scope:** Malaysia (attacker base) → Pakistan (victim residence) → Sweden/Singapore/Hong Kong (C2 infrastructure)
- **Primary Vector:** Social engineering via dating app → physical access → device cloning → DSU/GSI infrastructure → baseband exploitation

### Technical Anomalies
| Finding | Severity | Detectable by Standard Tools? |
|---------|----------|------------------------------|
| 9 device clones (same IMEI/serial) | **CRITICAL** | ❌ No (requires Google Account audit) |
| Android 16 GSI on Android 14 device | **CRITICAL** | ❌ No (requires ADB/DSU inspection) |
| 3 active QXDM baseband diagnostic interfaces | **CRITICAL** | ❌ No (requires AIDA64 or QPST) |
| Writable rescue partition (survives factory reset) | **HIGH** | ❌ No (requires partition audit) |
| Magisk root layer in boot ramdisk (shared across 3 OS environments) | **HIGH** | ❌ No (requires boot image extraction) |
| 52,773 account access events (April 2026) | **HIGH** | ⚠️ Partial (Google Account security review) |
| Emulator detection (491px screen width) | **MEDIUM** | ⚠️ Partial (Google Device Activity) |

### Structural Vulnerability Identified

> **End-of-support Android devices retain active DSU (Dynamic System Update) infrastructure that continues to receive current GSI (Generic System Image) builds from Google — creating a persistent, widening attack surface that outlives manufacturer security support timelines.**

This is not a bug. This is by design. And it is being exploited.

---

## 📊 Visualizations

### Chapter 1: Attack Analysis (14 figures)
- [Attack Campaign Timeline](visualizations/chapter_1/attack_timeline.png) — 550-day sustained operation, 5 phases
- [Device Clone Lifecycle](visualizations/chapter_1/clone_timeline.png) — 9 clones + 1 legitimate device, locale switching
- [VPN/Cloud Infrastructure](visualizations/chapter_1/vpn_cloud_infrastructure.png) — Mullvad, NordVPN, Alibaba Cloud, DigitalOcean
- [Access Volume Anomaly](visualizations/chapter_1/access_volume_anomaly.png) — 52,773 events, threshold breaches
- [Attack Infrastructure Map](visualizations/chapter_1/attack_infrastructure_map.png) — Geographic distribution
- [Technical Attack Flowchart](visualizations/chapter_1/attack_flowchart.png) — 6-phase vector analysis
- [Baseband Compromise Architecture](visualizations/chapter_1/baseband_compromise_architecture.png) — QXDM diagnostic exploitation
- [Persistence Mechanism Comparison](visualizations/chapter_1/persistence_mechanism_comparison.png) — Standard vs compromised reset
- [Forensic Evidence Board](visualizations/chapter_1/forensic_evidence_board.png) — RAK/CYB/2026/001 Addendum C
- [Complete Timeline with Baseband](visualizations/chapter_1/complete_timeline_with_baseband.png) — Full 600+ day chronology
- [Multi-Environment Boot Architecture](visualizations/chapter_1/multi_environment_boot_architecture.png) — DSU/GSI/Magisk
- [Remote Emulator Architecture](visualizations/chapter_1/remote_emulator_architecture.png) — Data flow model
- [Three Operational Models](visualizations/chapter_1/three_operational_models.png) — DSU/GSI exploitation comparison
- [C2 Channel Analysis](visualizations/chapter_1/c2_channel_analysis.png) — 6 independent channels

### Chapter 2: Defensive Countermeasures (2 figures)
- [Remediation Decision Flowchart](visualizations/chapter_2/ch2_remediation_flowchart.png)
- [Security Hardening Checklist](visualizations/chapter_2/ch2_security_hardening_checklist.png)

### Chapter 3: Legal Framework (2 figures)
- [Legal Framework Comparison](visualizations/chapter_3/ch3_legal_framework_comparison.png) — Malaysia vs Pakistan
- [Evidence Chain of Custody](visualizations/chapter_3/ch3_evidence_chain_of_custody.png)

### Chapter 4: Advanced Forensics (2 figures)
- [Forensic Tool Comparison Matrix](visualizations/chapter_4/ch4_forensic_tool_comparison.png) — 8 tools evaluated
- [Forensic Investigation Workflow](visualizations/chapter_4/ch4_forensic_investigation_workflow.png) — 6-phase procedure

---

## 🔍 Indicators of Compromise (IOCs)

See [evidence/IOCs.md](evidence/IOCs.md) for machine-readable IOCs including:
- IMEI/Serial patterns (truncated for privacy)
- VPN ASN identifiers (Hern Labs AB AS205016)
- Cloud server IP addresses (Alibaba Cloud, DigitalOcean)
- Emulator screen width artifacts (491px)
- Android ID patterns (clone registry)
- QXDM device paths (/dev/ffs-diag*)
- DSU build fingerprints (Android 16 GSI)

---

## 🛡️ Defensive Actions (If You Suspect Similar Compromise)

### IMMEDIATE (First 24 Hours)
1. **Quarantine device** in Faraday bag — do not power off if currently on
2. **Create new accounts** — do not reuse any credentials from compromised device
3. **Enable hardware 2FA** (YubiKey/Titan Key) — do not use SMS-based 2FA
4. **Replace SIM** with new eSIM (new IMSI) — do not transfer old SIM
5. **Document everything** — screenshots, timestamps, observations

### SHORT-TERM (1-7 Days)
6. **Purchase new device** from authorized retailer — do not restore from backup
7. **Replace router** or factory reset + firmware update — change all WiFi passwords
8. **Isolate networks** — create guest network for untrusted devices
9. **Use Signal/Wire** for sensitive communications — do not use WhatsApp
10. **Review Google Account** device activity for unknown devices

### LONG-TERM (Ongoing)
11. **Weekly audits** of account access, location history, device registrations
12. **Monthly permission reviews** — revoke unnecessary app access
13. **Quarterly baseband scans** using AIDA64 or similar tools
14. **Hardware security keys** for all critical accounts
15. **Network traffic monitoring** using Pi-hole or enterprise firewall

**See [Chapter 2](chapters/Chapter_2_Defensive_Countermeasures.md) for complete protocol.**

---

## ⚖️ Legal Framework

### Malaysia
- **Computer Crimes Act 1997** (Sections 3, 4, 5, 6, 9) — Unauthorized access, modification, interception, extra-territorial jurisdiction
- **Communications and Multimedia Act 1998** (Sections 232, 233, 234, 235) — Fraudulent use, improper use, interception, damage
- **Penal Code** (Sections 383, 384, 416, 420) — Extortion, cheating by personation
- **Cyber Security Act 2024** — National Cyber Security Committee, NACSA powers

### Pakistan
- **Prevention of Electronic Crimes Act (PECA) 2016** (Sections 3–10) — Unauthorized access, interference, interception, cyber terrorism
- **Pakistan Penal Code 1860** (Sections 378, 383, 419, 420) — Theft, extortion, cheating
- **Electronic Transactions Ordinance 2002** (Sections 38–40) — Unauthorized access, modification

**See [Chapter 3](chapters/Chapter_3_Legal_Framework.md) for prosecution pathways, evidence requirements, and cross-border coordination mechanisms.**

---

## 🔬 Forensic Tools Required

| Tool | Purpose | Cost | Baseband | DSU/GSI |
|------|---------|------|----------|---------|
| **AIDA64 Android** | Partition audit, QXDM detection | $ | ✅ Yes | ✅ Yes |
| **QPST/QFIL** | Baseband dump, NV backup | $ | ✅ Yes | ❌ No |
| **ADB** | DSU control, system inspection | Free | ⚠️ Partial | ✅ Yes |
| **Cellebrite UFED** | Full forensic extraction | $$$ | ⚠️ Partial | ❌ No |
| **Frida** | Runtime analysis | Free | ❌ No | ⚠️ Partial |

**See [Chapter 4](chapters/Chapter_4_Advanced_Forensics.md) for complete procedures, command sequences, and interpretation guidelines.**

---

## 📚 Sources and References

1. Zimperium Mobile Security Glossary — RAT operational mechanisms (2024)
2. Journal of Intelligent Information Systems (Springer, 2025) — Stegomalware sanitization
3. Italian Conference on CyberSecurity (2024) — Android stegomalware detection evasion
4. ACM Conference on Data and Application Security (2024) — Android stegomalware analysis
5. Pakistan Telecommunication Authority (2025) — IMEI tampering enforcement actions
6. Qualcomm CVE Database (2024–2025) — Closed-source component vulnerabilities (CVSS 9.1)
7. Google Android Security Team / Qualcomm (March 2026) — CVE-2026-21385 zero-day patch
8. Android Open Source Project Documentation — DSU, GSI, Project Treble, AVF
9. Rabah Khan GSI Research Paper (31 May 2026) — Remote Emulator Architecture

**See individual chapters for inline citations and full bibliographic details.**

---

## 🤝 Contributing

We welcome contributions in the following areas:

- **Technical corrections** — Fact-checking, CVE updates, tool compatibility
- **Translations** — Arabic, Urdu, Malay, and other languages for regional accessibility
- **Legal updates** — New legislation, case law, prosecution outcomes
- **Forensic tools** — Additional tool evaluations, procedure improvements
- **Victim resources** — Support organizations, counseling services, legal aid
- **IOCs** — New clone signatures, VPN patterns, cloud infrastructure

**See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.**

### Code of Conduct
- No doxxing or personal information
- No exploit code or proof-of-concept releases
- Focus on detection, defense, and education
- Respect victim privacy and safety
- Maintain professional, evidence-based discourse

---

## 📜 License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).

- **Attribution required** — Cite this repository when using findings
- **ShareAlike** — Derivatives must use same license
- **Commercial use permitted** — Security vendors, law enforcement, researchers
- **No additional restrictions** — Open access for maximum impact

**Why CC BY-SA 4.0?** This license ensures the knowledge cannot be enclosed by proprietary vendors. Security research must remain accessible to defenders everywhere, regardless of budget or jurisdiction.

---

## ⚠️ Disclaimer

This repository is provided for **educational and defensive purposes only**. All technical evidence has been extracted from Google Takeout exports, device configuration services, network access logs, and AIDA64 partition analysis. Personal identifiers have been redacted to protect privacy while preserving technical integrity.

- **No exploit code** is included
- **No proof-of-concept** is provided
- **No victim identification** is possible from published data
- **No attacker enablement** is intended

**If you are experiencing similar compromise:** Follow the defensive protocols in Chapter 2. Report to law enforcement (FIA Cyber Crime Wing in Pakistan, PDRM Cyber Crime Unit in Malaysia). Seek professional cybersecurity assistance.

---

## 📬 Contact

- **Security vulnerabilities:** See [SECURITY.md](SECURITY.md) for responsible disclosure
- **General inquiries:** Open a [GitHub Discussion](https://github.com/YOUR_USERNAME/RAK-CYB-2026-001/discussions)
- **Technical issues:** Open a [GitHub Issue](https://github.com/YOUR_USERNAME/RAK-CYB-2026-001/issues)
- **Private communication:** PGP key available in repository root (for sensitive matters)

---

## 🙏 Acknowledgments

- **Victim:** For courage in documenting and sharing this case for public awareness
- **Forensic examiners:** Who developed the baseband and DSU analysis techniques
- **Open source community:** AIDA64, QPST, ADB, Frida, Magisk developers
- **Legal scholars:** PECA 2016, CCA 1997, and Cyber Security Act 2024 analysts
- **Kimi K2.6 (Moonshot AI):** Independent technical review and confidence assessment

---

## 📅 Changelog

| Version | Date | Changes |
|---------|------|---------|
| v1.0.0 | 2026-06-09 | Initial release: 4 chapters + expert review + 20 visualizations |
| v1.1.0 | [Planned] | Community translations, additional IOCs, tool updates |
| v2.0.0 | [Planned] | Chapter 5: Victim Support; Chapter 6: International Cooperation |

---

## 🔗 Related Resources

- [Android Security Bulletin](https://source.android.com/security/bulletin) — Monthly patch updates
- [Qualcomm Product Security](https://www.qualcomm.com/support/product-security) — CVE disclosures
- [Google Project Zero](https://bugs.chromium.org/p/project-zero/issues/list) — Zero-day research
- [MITRE ATT&CK Mobile](https://attack.mitre.org/matrices/mobile/) — Mobile threat taxonomy
- [OWASP Mobile Security](https://owasp.org/www-project-mobile-security/) — Mobile security guidelines

---

**Repository:** [github.com/YOUR_USERNAME/RAK-CYB-2026-001](https://github.com/YOUR_USERNAME/RAK-CYB-2026-001)  
**Case Reference:** RAK/CYB/2026/001  
**Last Updated:** 2026-06-09  
**Status:** Active — accepting contributions and updates

---

> *"The campaign documented in this report is not an anomaly — it is a preview of the mobile threat landscape through 2030 and beyond."*
> — Chapter 1, Conclusion
