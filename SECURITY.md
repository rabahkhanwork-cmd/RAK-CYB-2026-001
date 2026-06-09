# Security Policy

## Supported Versions

This repository contains security research documentation, not software. As such, "versions" refer to content releases:

| Version | Status | Release Date | Notes |
|---------|--------|-------------|-------|
| v1.0.0 | ✅ Current | 2026-06-09 | Initial release: 4 chapters + expert review |
| v1.1.0 | 🔄 Planned | TBD | Community translations, IOC updates |
| v2.0.0 | 🔄 Planned | TBD | New chapters: Victim Support, International Cooperation |

---

## Reporting Security Vulnerabilities

### What to Report

We welcome responsible disclosure of:
- **New vulnerabilities** discovered through the research presented in this repository
- **Errors in defensive guidance** that could leave users vulnerable
- **Missing mitigations** for attack techniques documented in the case study
- **Inaccurate IOCs** that could lead to false negatives or false positives
- **Privacy concerns** in published content (unintentional PII exposure)

### What NOT to Report

- **Attack reproduction requests** — We do not provide exploit code or PoC
- **Social engineering attempts** — Report to law enforcement, not this repository
- **General cybersecurity questions** — Use GitHub Discussions instead
- **Legal advice requests** — Consult qualified legal professionals in your jurisdiction

### Responsible Disclosure Process

1. **Initial Contact:** Send encrypted email to security contact (see below) with:
   - Vulnerability description (high level, no exploit details)
   - Affected component (chapter, section, tool, procedure)
   - Severity assessment (Critical / High / Medium / Low)
   - Proposed mitigation or fix (if available)

2. **Acknowledgment:** We will acknowledge receipt within 72 hours

3. **Verification:** We will verify the vulnerability and assess impact (7-14 days)

4. **Coordination:** If the vulnerability affects a vendor (Google, Xiaomi, Qualcomm), we will coordinate responsible disclosure with the vendor (90-day standard deadline)

5. **Publication:** We will publish defensive guidance and mitigation simultaneously with vendor patch or at the end of the disclosure deadline

6. **Recognition:** You will be credited in the advisory (unless you prefer anonymity)

### Disclosure Timeline

| Phase | Timeline | Action |
|-------|----------|--------|
| Initial report | Day 0 | Researcher submits vulnerability |
| Acknowledgment | Day 0-3 | Repository maintainers confirm receipt |
| Verification | Day 3-14 | Verify vulnerability, assess impact |
| Vendor notification | Day 14 | Notify affected vendor with 90-day deadline |
| Patch development | Day 14-90 | Vendor develops and tests patch |
| Public disclosure | Day 90 | Publish defensive guidance and mitigation |
| CVE assignment | Day 90+ | Request CVE if applicable |

**Exceptions:** If the vulnerability is actively exploited in the wild, we may accelerate disclosure with vendor coordination.

---

## Security Contact

### PGP-Encrypted Email (Preferred)

```
Fingerprint: [YOUR_PGP_FINGERPRINT_HERE]
Key ID: [YOUR_KEY_ID_HERE]
Key Server: keys.openpgp.org
```

**Email:** security@your-domain.com (replace with your actual secure email)

**Subject line:** `[SECURITY] RAK-CYB-2026-001: [Brief description]`

**Body template:**
```
Vulnerability: [High-level description]
Component: [Chapter, section, tool, or procedure affected]
Severity: [Critical / High / Medium / Low]
Impact: [Who is affected and how]
Proposed mitigation: [If available]
Responsible disclosure: [Yes / No — have you notified vendor?]
```

### GitHub Security Advisory (Alternative)

For non-sensitive security matters, you may open a [GitHub Security Advisory](https://github.com/YOUR_USERNAME/RAK-CYB-2026-001/security/advisories) (private by default).

**Note:** GitHub Security Advisories are visible to repository maintainers only. Use this for lower-severity issues or if PGP encryption is not available.

---

## PGP Key

```
-----BEGIN PGP PUBLIC KEY BLOCK-----

[YOUR_PGP_PUBLIC_KEY_HERE]

-----END PGP PUBLIC KEY BLOCK-----
```

**Key verification:**
- Fingerprint available above
- Published on keys.openpgp.org
- Cross-signed by [trusted community members if applicable]

---

## Security Best Practices for Contributors

### When Submitting Content
1. **Verify sources:** Ensure all CVEs, vulnerabilities, and attack techniques are from reputable sources
2. **Anonymize data:** Remove all personal information before publication
3. **No exploit code:** Do not include proof-of-concept or exploit code in submissions
4. **Defensive focus:** Emphasize detection, mitigation, and prevention
5. **Legal review:** Consult legal counsel before publishing sensitive findings

### When Using This Repository
1. **Verify integrity:** Check file hashes and signatures before using forensic procedures
2. **Test in isolation:** Test tools and procedures in isolated environments before production use
3. **Legal compliance:** Ensure your use of these techniques complies with local laws
4. **Professional consultation:** Consult certified forensic examiners for legal proceedings
5. **Vendor coordination:** Coordinate with device manufacturers before public disclosure

---

## Incident Response

If you believe you have been targeted by a similar attack:

### IMMEDIATE (0-1 hour)
1. **Do NOT panic** — Maintain clear thinking for evidence preservation
2. **Document current state** — Screenshot everything visible on screen
3. **Enable airplane mode** (if device is on) — Prevents remote commands
4. **Do NOT factory reset** — Destroys evidence, may not remove baseband compromise
5. **Contact legal counsel** — Before any action that could affect legal proceedings

### SHORT-TERM (1-24 hours)
6. **Quarantine device** — Faraday bag, power off if safe, chain of custody log
7. **Create new accounts** — From a clean device, do not reuse credentials
8. **Enable hardware 2FA** — YubiKey or Titan Key, not SMS-based
9. **Report to law enforcement** — FIA Cyber Crime Wing (Pakistan), PDRM Cyber Crime Unit (Malaysia)
10. **Preserve evidence** — Router logs, ISP records, Google Takeout, CCTV footage

### ONGOING
11. **Follow Chapter 2 protocols** — Complete remediation and monitoring procedures
12. **Seek victim support** — Counseling, legal aid, victim advocacy organizations
13. **Monitor for recurrence** — New devices, new accounts, new networks
14. **Contribute to community** — Share anonymized findings to help others

**See [Chapter 2: Defensive Countermeasures](chapters/Chapter_2_Defensive_Countermeasures.md) for complete protocol.**

---

## Security Research Ethics

This repository adheres to the following ethical principles:

1. **Do No Harm:** All research is defensive. We do not enable attacks.
2. **Privacy Protection:** Victim anonymity is paramount. No PII is published.
3. **Responsible Disclosure:** Vulnerabilities are reported to vendors before public disclosure.
4. **Accessibility:** Knowledge is shared openly for maximum defensive impact.
5. **Accuracy:** Claims are evidence-based, sourced, and peer-reviewed where possible.
6. **Community Benefit:** Research serves the broader security community, not individual gain.

---

## Acknowledgments

We thank the security researchers, forensic examiners, and victim advocates who have contributed to mobile security knowledge. This repository stands on their work.

**Hall of Fame:**
- [Reserved for responsible disclosure contributors]

---

**Last Updated:** 2026-06-09  
**Next Review:** 2026-09-09 (quarterly)  
**Maintainer:** [Your name or organization]  
**Contact:** security@your-domain.com (PGP-encrypted)
