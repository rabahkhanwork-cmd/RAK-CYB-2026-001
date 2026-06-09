# Contributing to RAK-CYB-2026-001

Thank you for your interest in contributing to this security research repository. This document provides guidelines for contributions, issue reporting, and community engagement.

## 🎯 Contribution Areas

### 1. Technical Corrections
- CVE updates and corrections
- Tool compatibility testing and results
- Forensic procedure improvements
- Android version/build-specific variations
- Baseband analysis technique refinements

**How to contribute:** Open a Pull Request with corrected content, citing sources.

### 2. Translations
- Arabic (ar) — Critical for Middle East and North Africa accessibility
- Urdu (ur) — Critical for Pakistan and South Asia accessibility
- Malay (ms) — Critical for Malaysia and Southeast Asia accessibility
- Mandarin (zh) — Critical for China and East Asia accessibility
- Hindi (hi) — Critical for India and South Asia accessibility
- French (fr) — Critical for Francophone Africa and Europe
- Spanish (es) — Critical for Latin America accessibility

**How to contribute:**
1. Fork the repository
2. Create `translations/[language_code]/` directory
3. Translate one chapter at a time (maintain technical accuracy)
4. Include original English technical terms in parentheses for clarity
5. Submit Pull Request with "[LANG] Translation: Chapter X" title

### 3. Legal Updates
- New legislation affecting mobile cybercrime prosecution
- Case law and prosecution outcomes (anonymized)
- Cross-border coordination mechanism improvements
- Jurisdiction-specific procedure updates

**How to contribute:** Open an Issue with "Legal Update: [Jurisdiction]" title, include citation and source.

### 4. Forensic Tool Evaluations
- Additional tool testing (open source and commercial)
- Procedure variations for different device models
- New detection techniques for DSU/GSI exploitation
- Baseband analysis tool comparisons

**How to contribute:** Open a Pull Request with tool evaluation report, including test methodology and results.

### 5. Victim Resources
- Support organizations (by region)
- Counseling and trauma resources
- Legal aid directories (by jurisdiction)
- Financial recovery guidance
- Safety planning resources

**How to contribute:** Open an Issue with "Resource Addition: [Category]" title, include organization name, contact, and verification.

### 6. Indicators of Compromise (IOCs)
- New clone device signatures
- VPN provider patterns
- Cloud infrastructure indicators
- Emulator artifact variations
- Baseband diagnostic interface patterns

**How to contribute:** Open a Pull Request updating `evidence/IOCs.md` with new patterns, including detection methodology.

---

## 📝 Pull Request Guidelines

### Format
1. **Title:** `[CATEGORY] Brief description` (e.g., "[TECH] Fix CVE-2026-21385 reference")
2. **Description:** 
   - What changed and why
   - Sources or evidence supporting the change
   - Impact assessment (who benefits, what risk)
3. **Files changed:** List all modified files
4. **Testing:** How was the change verified (if applicable)

### Content Standards
- **Evidence-based:** All claims must be supported by sources, CVEs, or reproducible testing
- **Anonymized:** No personal information, real names, or identifiable details
- **Accessible:** Technical terms explained for non-specialist audience
- **Cited:** Academic papers, manufacturer documentation, or official reports preferred
- **Neutral:** No advocacy, political statements, or victim-blaming

### Review Process
1. Submit Pull Request
2. Automated checks (markdown linting, link validation)
3. Community review (minimum 1 reviewer for minor changes, 2 for major)
4. Maintainer approval (for final merge)
5. Merge and release (tagged in changelog)

---

## 🐛 Issue Reporting

### Bug Reports (Technical Errors)
**Title:** `[BUG] Brief description`  
**Template:**
```
**Location:** Chapter X, Section Y, Paragraph Z
**Error:** What is incorrect
**Correction:** What should be stated instead
**Evidence:** Source, CVE, or test result supporting correction
**Impact:** Who is affected and how
```

### Feature Requests (New Content)
**Title:** `[FEATURE] Brief description`  
**Template:**
```
**Category:** Technical / Legal / Resource / Translation / Other
**Description:** What should be added or changed
**Rationale:** Why this benefits the community
**Proposed content:** Draft text or outline (if available)
**Sources:** Supporting documentation or references
```

### Security Vulnerabilities
**Title:** `[SECURITY] Brief description`  
**Template:**
```
**Vulnerability:** What security issue exists in the repository
**Severity:** Critical / High / Medium / Low
**Impact:** Who could be affected and how
**Remediation:** Proposed fix or mitigation
**Responsible disclosure:** Have you followed responsible disclosure practices?
```

**For sensitive security matters:** See [SECURITY.md](SECURITY.md) for PGP-encrypted contact.

---

## 💬 Discussion Guidelines

### GitHub Discussions (Enabled)
- **Q&A:** Technical questions about attack methodology, detection, or defense
- **Ideas:** Proposals for new chapters, sections, or features
- **Show and Tell:** Share your own forensic findings, tool evaluations, or case studies
- **General:** Community building, networking, resource sharing

### Discussion Rules
1. **Respectful:** No harassment, doxxing, or personal attacks
2. **Evidence-based:** Claims require support; speculation labeled as such
3. **Constructive:** Criticism is welcome when accompanied by improvement suggestions
4. **On-topic:** Keep discussions relevant to mobile security, forensics, or victim support
5. **Safe:** No information that could endanger victims or enable attackers

---

## 🏷️ Commit Message Format

```
[TYPE] Brief description (max 50 chars)

Detailed explanation (if needed, wrap at 72 chars)
- Bullet points for multiple changes
- Reference issues: Fixes #123, Relates to #456

Signed-off-by: Your Name <your.email@example.com>
```

**Types:**
- `[TECH]` — Technical correction or update
- `[LEGAL]` — Legal framework addition or update
- `[TRANS]` — Translation contribution
- `[DOC]` — Documentation improvement
- `[IOCS]` — Indicator of Compromise update
- `[VIS]` — Visualization addition or update
- `[FIX]` — Bug fix or error correction
- `[CHORE]` — Maintenance, dependency update, formatting

---

## 🌐 Translation Guidelines

### Priority Languages (by regional impact)
1. **Urdu (ur)** — Pakistan (primary victim jurisdiction), India
2. **Malay (ms)** — Malaysia (attacker jurisdiction), Indonesia, Singapore
3. **Arabic (ar)** — Middle East, North Africa, cybersecurity community
4. **Mandarin (zh)** — China, Taiwan, Singapore (major device manufacturing)
5. **Hindi (hi)** — India (major device market, growing cybersecurity sector)

### Translation Standards
- **Accuracy:** Technical terms must be precisely translated; when no equivalent exists, use English term with explanation
- **Consistency:** Maintain consistent terminology across all chapters
- **Cultural sensitivity:** Adapt examples and references for local context while preserving technical accuracy
- **Legal accuracy:** Jurisdiction-specific legal terms must be verified by local legal professionals
- **Review:** Each translation requires review by a second native speaker before merge

### Translation Workflow
1. Claim a chapter by opening an Issue: "[TRANS-ur] Claim: Chapter 1"
2. Fork repository, create branch: `trans/ur/chapter-1`
3. Translate using provided template (maintain markdown structure)
4. Submit Pull Request with "[TRANS-ur] Chapter 1: Anatomy of Android RAT" title
5. Community review by native speakers (minimum 1 reviewer)
6. Maintainer approval and merge

---

## ⚖️ Legal and Ethical Guidelines

### What We Accept
- ✅ Evidence-based technical corrections
- ✅ Defensive tool evaluations and procedures
- ✅ Legal framework updates and analysis
- ✅ Victim support resources (verified organizations)
- ✅ Translation contributions
- ✅ IOC pattern updates

### What We Reject
- ❌ Exploit code or proof-of-concept releases
- ❌ Instructions for reproducing the attack
- ❌ Personal information or doxxing attempts
- ❌ Victim-blaming or harassment
- ❌ Political advocacy unrelated to cybersecurity
- ❌ Commercial promotion without community benefit
- ❌ Unverified claims without evidence

### Responsible Disclosure
- If you discover a new vulnerability through this research, follow responsible disclosure:
  1. Notify affected vendor (Google, Xiaomi, Qualcomm) with 90-day deadline
  2. Coordinate with vendor on public disclosure timeline
  3. Publish defensive guidance (detection, mitigation) simultaneously with patch
  4. Do NOT publish exploit code or detailed reproduction steps

---

## 🙏 Recognition

Contributors will be recognized in:
- Repository README (Contributors section)
- Release notes for each version
- Academic citations (if applicable)
- Conference presentations (if applicable)

**No financial compensation** is available. This is a community-driven security research project.

---

## 📬 Contact

- **General questions:** GitHub Discussions
- **Technical issues:** GitHub Issues
- **Private matters:** PGP-encrypted email (key in repository root)
- **Security vulnerabilities:** See [SECURITY.md](SECURITY.md)

---

Thank you for helping make mobile security knowledge accessible to defenders everywhere.

*"Security through obscurity is not security. Knowledge shared is vulnerability reduced."*
