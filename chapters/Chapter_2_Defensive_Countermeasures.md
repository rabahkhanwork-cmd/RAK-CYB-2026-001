
# CHAPTER 2: DEFENSIVE COUNTERMEASURES AND RECOVERY PROTOCOLS
## Post-Compromise Remediation for Baseband-Level and DSU/GSI Attack Infrastructure

---

**Document Classification:** Public Technical Report  
**Case Reference:** RAK/CYB/2026/001  
**Report Date:** June 2026  
**Version:** 1.0  

---

## EXECUTIVE SUMMARY

This chapter provides actionable defensive countermeasures and recovery protocols for victims of the attack class documented in Chapter 1 — specifically, compromises involving device cloning, DSU/GSI multi-environment persistent infrastructure, and baseband-level diagnostic exploitation. The recommendations are derived from the forensic evidence presented in Chapter 1, cross-referenced with industry best practices, academic literature on mobile security hardening, and legal requirements for evidence preservation in Malaysia and Pakistan.

The central challenge in remediating this class of attack is that **standard defensive measures are ineffective**. Factory reset, password changes, and application removal do not remove baseband implants, tampered rescue partitions, or DSU/Magisk boot partition modifications. The victim could wipe their device a hundred times and remain compromised. This chapter addresses the **full remediation stack** from immediate quarantine through long-term monitoring, with explicit attention to the legal evidence preservation requirements that complicate the "destroy and replace" instinct.

---

## 1. THE REMEDIATION DILEMMA: WHY STANDARD MEASURES FAIL

### 1.1 The Factory Reset Myth

For most mobile users and even many security professionals, the factory reset is the go-to response to suspected compromise. The assumption is that wiping the device to its factory state removes all malicious software and restores the device to a trusted baseline. This assumption is **catastrophically wrong** for the attack class documented in Chapter 1.

A standard factory reset operates at the **OS layer** — it wipes the /data and /cache partitions and reinstalls the system partition from the recovery image. It does **not** touch:

- **Baseband firmware**: The Qualcomm modem processor and its diagnostic interfaces (QXDM) operate below the OS entirely
- **Rescue partition**: If tampered with, the recovery environment may reinstall malicious components during the "reset" process
- **Boot partition ramdisk**: Magisk and LSPosed modifications persist here, initializing before any OS loads
- **DSU dynamic partitions**: GSI environments exist outside the primary OS partition structure
- **Modem configuration stores**: QMCS and SPUNVM modifications survive OS reinstallation

The June 2026 baseband forensic discovery (Addendum C) revealed that the rescue partition on the subject device was mounted **READ-WRITE** — a state that enables modification of the recovery environment. When a user initiates factory reset, the device boots into the recovery partition to execute the wipe. If this partition has been tampered with, the reset process can be subverted — the system may appear to wipe while actually preserving or reinstalling malicious components. This is a documented persistence technique used by advanced threat actors to survive factory resets. [cite: web_search:17#4]

### 1.2 The Credential Change Trap

Changing passwords, enabling 2FA, and revoking app permissions are standard post-compromise responses. These measures are **necessary but insufficient** when the attacker maintains:

- **Device clones** with the victim's IMEI and serial number, which can re-authenticate to Google services
- **SIM clones** that receive SMS-based 2FA codes intended for the victim
- **Baseband access** that intercepts SMS and voice calls before they reach the OS layer
- **DSU/GSI environments** that operate with the victim's OAuth tokens and account credentials

The attacker documented in Chapter 1 cloned the victim's Malaysian Maxis SIM card, enabling receipt of SMS messages (including 2FA codes) intended for the victim. Even after the victim changed passwords and enabled 2FA, the attacker could intercept the verification codes via the cloned SIM and maintain account access. This is a well-documented attack vector: SIM cloning exploits vulnerabilities in the GSM authentication protocol, specifically the extraction of the Ki (authentication key) from the SIM card. [cite: web_search:9#3]

### 1.3 The Device Replacement Paradox

Replacing the compromised device with a new one is the most effective remediation step — but it introduces a new risk: **credential reuse**. If the victim restores from a backup, reuses passwords, or transfers the old SIM to the new device, the attacker may maintain access through:

- **Cloud account compromise**: If the Google account itself is compromised, the new device syncs the attacker's access
- **Network compromise**: If the home WiFi network or router is compromised, the new device connects to a hostile network
- **Bluetooth pairing**: If old Bluetooth pairings are transferred, compromised peripherals may reintroduce the attack vector
- **Social engineering**: The attacker may repeat the social engineering approach with the new device

Complete remediation requires **isolation at every layer** — device, account, network, and communication channel.

---

## 2. IMMEDIATE ACTIONS: THE FIRST 24 HOURS

### 2.1 Device Quarantine and Evidence Preservation

If legal proceedings are pending or contemplated, the compromised device must be **quarantined for forensic examination** rather than destroyed or wiped. The chain of custody requirements for digital evidence are stringent, and any action that modifies the device state may render evidence inadmissible.

**Step 1: Power State Assessment**
- If the device is ON: Enable airplane mode immediately (if safe to do so) to prevent remote wipe commands or data exfiltration
- If the device is OFF: Do NOT power it on. The current power state is forensic evidence
- If the battery is critical: Connect to power through a Faraday bag with a charging cable

**Step 2: Faraday Bag Isolation**
- Place the device in an RF-shielded Faraday bag immediately
- Seal the bag with tamper-evident tape
- Label with case number, date, time, and handler initials
- Maintain the bag sealed until forensic examination
- Store in a secure, climate-controlled environment
- Log every access to the storage location

**Step 3: Documentation**
- Photograph the device in situ before moving it: serial number, IMEI label, physical state, screen display
- Record exact time, date, and location of seizure
- Document who seized the device, who witnessed, and environmental conditions
- Identify all associated devices: chargers, cables, SIM cards, SD cards

**Step 4: Chain of Custody Log**
- Maintain a chronological log of ALL evidence handling
- Record: who, what, when, where, why for each access
- Use a standardized evidence handling form
- Require signature for every transfer of custody
- Include digital signatures and timestamps where possible
- Consider blockchain-based custody logging (emerging best practice)

### 2.2 Account Isolation (Parallel to Quarantine)

While the device is being quarantined, immediate account isolation must begin:

**Step 1: Create New Accounts**
- Create a NEW Google account with NO connection to previous credentials
- Use a NEW email address (not a variation of the old address, e.g., not oldname+1@gmail.com)
- Do NOT reuse ANY passwords from compromised accounts
- Use a password manager with a NEW master password

**Step 2: Enable Hardware 2FA**
- Enable FIDO2/WebAuthn hardware security keys (YubiKey, Titan Security Key) for all critical accounts
- Do NOT use SMS-based 2FA — SIM cloning risk remains active
- Do NOT use app-based TOTP (Google Authenticator, Authy) on the new device until it is fully secured
- Register multiple hardware keys for redundancy

**Step 3: Revoke and Audit**
- Review and revoke ALL third-party app permissions from the old Google account
- Check Google Account security settings for unknown devices, apps, and access locations
- Review "Recent security activity" for suspicious events
- Remove all payment methods from compromised accounts

**Step 4: Communication Channel Isolation**
- Use Signal or Wire for sensitive communications (end-to-end encrypted, no cloud backup)
- Verify safety numbers for all Signal contacts
- Do NOT use WhatsApp on the new device (compromised APK history from Chapter 1)
- Enable disappearing messages for sensitive conversations
- Use ProtonMail or Tutanota for email (encrypted, no Google infrastructure)
- Do NOT forward emails from old account to new account
- Notify contacts of new communication channels via OUT-OF-BAND method (in-person, written note, trusted intermediary)

### 2.3 Network Sanitization

The attacker had physical access to the victim's residence in both Malaysia and Pakistan, and may have compromised the network infrastructure:

**Step 1: Router Replacement or Sanitization**
- Replace the home router with a NEW device (preferred)
- OR factory reset the existing router AND update firmware to latest version
- Change ALL WiFi network names (SSIDs) and passwords
- Disable WPS (WiFi Protected Setup) — known vulnerability
- Enable WPA3 encryption (or WPA2-AES minimum)
- Change router admin password from default
- Review connected devices list for unknown MAC addresses
- Disable remote management access on router

**Step 2: Network Segmentation**
- Create a separate guest network for untrusted devices
- Isolate IoT devices (smart TVs, cameras, speakers) on their own VLAN
- Monitor network traffic for unusual patterns (DNS requests to unknown domains, beaconing behavior)

**Step 3: ISP Coordination**
- Request new public IP address from ISP (if dynamic, power cycle modem; if static, request change)
- Review ISP logs for unauthorized access or unusual traffic patterns
- Report suspected compromise to ISP abuse team

---

## 3. DEVICE REPLACEMENT PROTOCOL

### 3.1 Procurement and Verification

**Purchase from Authorized Retailer**
- Buy from manufacturer-authorized retailer or carrier store
- Avoid second-hand devices (unknown history, potential pre-compromise)
- Verify device is sealed in original packaging
- Check manufacturing date — avoid devices that have been in inventory for extended periods

**Bootloader Verification**
- Verify bootloader is LOCKED on first boot
- Check that OEM unlocking is DISABLED in Developer Options
- Verify verified boot (dm-verity) is ENABLED
- Check build fingerprint matches manufacturer-signed image (can be verified via ADB: adb shell getprop ro.build.fingerprint)

**Do NOT Restore from Backup**
- Configure the new device as NEW — do not restore from Google Backup, iCloud Backup, or local backup
- Do not transfer apps, settings, or data from the old device
- Manually reinstall only essential applications from official stores (Google Play, Apple App Store)
- Do NOT install WhatsApp or any messaging app that was compromised on the old device

### 3.2 SIM and Connectivity

**Request New eSIM**
- Do NOT transfer the physical SIM from the compromised device
- Request a NEW eSIM from the carrier with a NEW IMSI (International Mobile Subscriber Identity)
- eSIM technology is significantly more resistant to cloning than physical SIM cards
- If eSIM is not available, request a new physical SIM with new IMSI and destroy the old SIM

**Bluetooth and Peripheral Isolation**
- Do NOT pair with old Bluetooth devices (headphones, speakers, car systems)
- Pair ONLY new peripherals that have never been connected to the compromised device
- Be aware that Bluetooth pairing history can be exploited for reconnection attacks

---

## 4. ONGOING MONITORING AND DETECTION

### 4.1 Weekly Reviews

**Google Account Device Activity**
- Review Google Account "Your devices" section WEEKLY
- Look for unexpected Android IDs, unknown device models, or unfamiliar locations
- Check for devices with screen widths inconsistent with your physical device
- Monitor for locale changes (e.g., en-US appearing on a device normally set to en-GB)

**Location History Audit**
- Review Google Timeline for unknown access points
- Check for locations you did not visit (indicates clone device activity)
- Cross-reference location data with your own travel records

**Access Event Log**
- Maintain a personal log of ALL device access events (when you used the device, what apps, what networks)
- Use this log for anomaly detection — if the device shows activity when you were not using it, investigate

### 4.2 Monthly Reviews

**App Permission Audit**
- Review ALL app permissions MONTHLY
- Revoke unnecessary access (location, camera, microphone, contacts)
- Check for apps you did not install
- Verify app signatures match official developers (use APK Analyzer or similar)

**Battery and Performance Monitoring**
- Monitor battery usage for unexplained background drain
- Check for apps consuming excessive CPU or network resources in background
- Look for device heating during idle periods (indicates hidden activity)

**Network Traffic Analysis**
- Use router-level monitoring (Pi-hole, OpenWrt, or enterprise firewall) to track DNS requests and outbound connections
- Look for beaconing patterns (regular connections to unknown domains)
- Monitor for unusual data upload volumes during sleep hours

### 4.3 Quarterly Deep Scans

**Baseband Diagnostic Scan**
- Use AIDA64 Android or similar low-level diagnostic tool to scan for QXDM interfaces
- Check /dev/ffs-diag* entries — any presence is anomalous on a consumer device
- Verify rescue partition mount state (should be READ-ONLY or not mounted)
- Check modem configuration partitions (QMCS, SPUNVM) for unauthorized modifications

**System Property Audit**
- Dump all system properties (adb shell getprop) and scan for:
  - ro.debuggable=1 (should be 0 on production devices)
  - ro.secure=0 (should be 1 on production devices)
  - BUILD_TYPE=userdebug (should be user on production devices)
  - Any property containing "test", "debug", or "eng"

**DSU Loader Verification**
- Check Developer Options for DSU Loader presence (should be visible or not present on most devices)
- If hidden, use Hidden Settings or ADB to verify DSU slot status
- Check for unexpected GSI installations or dynamic partition configurations

---

## 5. LONG-TERM SECURITY POSTURE (2026–2030)

### 5.1 Zero-Trust Mobile Architecture

The compromise documented in Chapter 1 demonstrates that **device-centric security is insufficient**. A zero-trust approach treats all mobile devices as potentially compromised and implements continuous verification:

- **Hardware security keys** for all critical authentication (cannot be cloned or phished)
- **Certificate-based VPN** rather than password-based (prevents credential replay)
- **Application sandboxing** using Android Work Profile or enterprise MDM
- **Network micro-segmentation** isolating devices by function and trust level
- **Continuous monitoring** rather than periodic scans

### 5.2 eSIM and Hardware Attestation

The transition to eSIM technology eliminates the physical SIM cloning vector. Future devices should mandate:
- **eSIM-only** configuration (no physical SIM slot)
- **Hardware-backed attestation** (TEE, SE, Titan M chip) that cannot be bypassed by custom ROMs or GSI environments
- **Verified boot chain** that cryptographically verifies every boot stage

### 5.3 DSU Infrastructure Awareness

The structural vulnerability identified in Chapter 1 — end-of-support devices retaining active DSU infrastructure — requires industry-wide attention:
- **Consumer education** about DSU risks on older devices
- **Manufacturer responsibility** to disable DSU on end-of-support devices or provide clear security warnings
- **Regulatory pressure** to include DSU status in device security audits

---

## 6. PSYCHOLOGICAL AND OPERATIONAL SECURITY

### 6.1 Victim Support

A 600+ day sustained attack campaign causes significant psychological trauma. Victims should:
- Seek professional counseling specializing in cybercrime trauma
- Join victim support groups (e.g., Cyber Civil Rights Initiative, Victim Support UK)
- Document emotional and financial impact for legal proceedings
- Maintain a "safe" communication channel with trusted contacts (in-person, written notes)

### 6.2 Operational Security (OPSEC) for Victims

- Assume the attacker monitors all digital communications
- Use out-of-band methods for sensitive coordination (legal counsel, law enforcement)
- Vary daily routines to prevent physical tracking
- Be aware of surveillance indicators (unusual vehicles, repeated faces, electronic interference)
- Maintain a "go bag" with essential documents, cash, and clean communication devices

---

## 7. CONCLUSION

The attack class documented in Chapter 1 — baseband-level compromise combined with DSU/GSI persistent infrastructure — renders standard remediation measures ineffective. Victims must adopt a **layered, comprehensive recovery protocol** that addresses device, account, network, and communication channel isolation simultaneously.

The key principles are:
1. **Quarantine, don't destroy** (if legal proceedings are pending)
2. **Replace, don't restore** (new device, new accounts, new credentials)
3. **Isolate, don't reconnect** (new networks, new peripherals, new SIM)
4. **Monitor, don't assume** (ongoing verification, not one-time cleanup)
5. **Document, don't forget** (evidence preservation, legal preparation, psychological support)

The defensive recommendations in this chapter are not theoretical — they are derived from the specific forensic evidence of Case RAK/CYB/2026/001 and represent the minimum necessary response to this class of threat. As mobile devices continue to absorb the functions of wallets, identity documents, and primary computing platforms, the stakes of compromise will only increase. The protocols documented here must become standard practice for all mobile users, not just those who have already been victimized.

---

**Next Chapter:** Chapter 3 — Legal Framework and Law Enforcement Engagement
