
# CHAPTER 4: ADVANCED FORENSIC TECHNIQUES FOR MOBILE DEVICE INVESTIGATION
## Specialized Procedures for DSU/GSI Infrastructure and Baseband-Level Compromise

---

**Document Classification:** Public Technical Report  
**Case Reference:** RAK/CYB/2026/001  
**Report Date:** June 2026  
**Version:** 1.0  

---

## EXECUTIVE SUMMARY

This chapter provides advanced forensic techniques for investigating mobile device compromises involving Dynamic System Update (DSU)/Generic System Image (GSI) infrastructure exploitation and baseband-level diagnostic interface manipulation. The techniques described are derived from the forensic evidence presented in Chapter 1, cross-referenced with industry-standard forensic methodologies, academic literature on mobile forensics, and manufacturer technical documentation.

The central challenge in investigating this class of attack is that **standard forensic tools and procedures are inadequate**. Cellebrite UFED, GrayKey, and XRY — the industry-standard tools for mobile forensic extraction — are designed to acquire data from the primary operating system partition. They do not detect, acquire, or analyze:

- DSU dynamic partitions containing GSI environments
- Boot partition ramdisk modifications (Magisk, LSPosed)
- Baseband firmware and diagnostic interfaces (QXDM)
- Modem configuration stores (QMCS, SPUNVM)
- Rescue partition tampering
- Remote emulator client artifacts

This chapter addresses the **full forensic stack** from pre-acquisition planning through specialized baseband analysis, with explicit tool recommendations, command sequences, and interpretation guidelines. All techniques are validated against the specific device model in Case RAK/CYB/2026/001 (Xiaomi 11T Pro, vili, Snapdragon 888, Android 14/HyperOS) but are applicable to any Treble-compliant Qualcomm device.

---

## 1. FORENSIC TOOL COMPARISON AND SELECTION

### 1.1 Standard Forensic Tools: Limitations for This Case

**Cellebrite UFED (Universal Forensic Extraction Device)**
- Capabilities: Logical extraction, physical extraction, file system dump, password bypass, cloud data acquisition
- Baseband Support: Partial (modem dump via QPST integration, but not native)
- DSU/GSI Support: No (primary OS partition only)
- Cost: $$$ (Enterprise, law enforcement pricing)
- **Assessment:** Essential for standard forensic acquisition but insufficient for this case. Must be supplemented with specialized tools.

**GrayKey**
- Capabilities: iOS full filesystem, iOS keychain, Android logical, Android file system
- Baseband Support: No (iOS-focused tool)
- DSU/GSI Support: No
- Cost: $$$ (Law enforcement only, restricted sale)
- **Assessment:** Not applicable to this Android case. iOS-focused architecture does not support Qualcomm baseband or Android DSU.

**XRY (MSAB)**
- Capabilities: Logical extraction, physical extraction, cloud recovery, drone data, IoT devices
- Baseband Support: Partial (SIM/UICC data only, not diagnostic interfaces)
- DSU/GSI Support: No (primary OS only)
- Cost: $$$ (Enterprise pricing)
- **Assessment:** Broader device support than Cellebrite but same limitation for DSU/GSI and baseband.

### 1.2 Specialized Tools: Required for This Case

**AIDA64 Android**
- Capabilities: System information, partition audit, device tree analysis, sensor data, network information
- Baseband Support: Yes (QXDM interface detection, modem status)
- DSU/GSI Support: Yes (DSU slot detection, dynamic partition status)
- Cost: $ (Consumer app, ~$5-10)
- **Assessment:** Critical first-line tool for rapid anomaly detection. The partition audit function (Directories → System) revealed the QXDM interfaces, rescue partition mount state, and modem configuration stores in Case RAK/CYB/2026/001. Inexpensive, non-destructive, and requires no root access.

**QPST (Qualcomm Product Support Tools) / QFIL (Qualcomm Flash Image Loader)**
- Capabilities: Qualcomm flash, baseband dump, NV item read, EFS backup, firmware restore
- Baseband Support: Yes (full baseband access via DIAG protocol)
- DSU/GSI Support: No (firmware tool, not OS-level)
- Cost: $ (Developer/service tool, free with Qualcomm developer account)
- **Assessment:** Essential for baseband forensic analysis. QPST's QCN backup function captures Non-Volatile (NV) items including modem configuration, IMEI, and network parameters. QFIL can dump the NON-HLOS.bin (baseband firmware image) for offline analysis.

**Android Debug Bridge (ADB)**
- Capabilities: Shell access, logcat, file transfer, package management, screen capture, DSU control
- Baseband Support: Partial (radio logs via logcat, diag port access with root)
- DSU/GSI Support: Yes (DSU slot listing, GSI installation/removal, dynamic partition inspection)
- Cost: Free (Developer tool, part of Android SDK)
- **Assessment:** Essential for DSU/GSI analysis and live system inspection. Commands: `adb shell gsi_tool list`, `adb shell getprop`, `adb logcat -b radio`.

**Magisk + LSPosed**
- Capabilities: Root access, module framework, Zygote hooking, system modification, root hiding
- Baseband Support: No (OS-level only)
- DSU/GSI Support: Yes (DSU module support, GSI modification)
- Cost: Free (Open source)
- **Assessment:** Required for deep system inspection on a rooted device. LSPosed modules can hook system calls to detect hidden activity. However, using Magisk on a forensic device modifies the system — must be used only after standard acquisition is complete.

**Frida**
- Capabilities: Dynamic instrumentation, API hooking, runtime analysis, memory dump, crypto analysis
- Baseband Support: No (user-space only)
- DSU/GSI Support: Yes (if root available)
- Cost: Free (Open source)
- **Assessment:** Powerful for runtime analysis of suspicious applications. Can hook JavaScript into running processes to intercept API calls, network requests, and encryption operations.

### 1.3 Recommended Tool Stack for This Case

**Primary Stack (Minimum Viable):**
1. AIDA64 Android (partition audit, QXDM detection, DSU discovery)
2. QPST/QFIL (baseband dump, NV backup, firmware analysis)
3. ADB (DSU control, system property dump, log collection)

**Secondary Stack (Enhanced Analysis):**
4. Cellebrite UFED (full forensic extraction, cloud data, legal admissibility)
5. Frida (runtime analysis of suspicious apps)
6. Magisk + LSPosed (deep system inspection, Zygote hooking — post-acquisition only)

**Not Applicable:**
- GrayKey (iOS-focused)
- Standard antivirus/endpoint detection (OS-level only, misses baseband and DSU)

---

## 2. PRE-ACQUISITION PLANNING

### 2.1 Legal Authority Verification

Before any forensic acquisition, verify legal authority:
- **Warrant**: Search warrant issued by competent court
- **Consent**: Written consent from device owner
- **Exigent circumstances**: Imminent threat to life or property
- **Statutory authority**: Specific powers under cybercrime legislation (CCA 1997, PECA 2016)

**Document:** Warrant number, issuing court, date, scope of authority, executing officer.

### 2.2 Device State Assessment

**Power State:**
- ON: Document screen display, active apps, notifications. Enable airplane mode if safe (prevents remote wipe/commands).
- OFF: Do NOT power on. Maintain power state for RAM capture if possible (cold boot attack, chip-off).
- LOCKED: Document lock type (PIN, pattern, fingerprint, face). Attempt legal unlock methods before forced extraction.

**Physical State:**
- Photograph: Front, back, sides, ports, SIM tray, SD card slot
- Document: Serial number, IMEI (from label), physical damage, modifications
- Collect: Chargers, cables, cases, SIM cards, SD cards, associated peripherals

**Environmental Conditions:**
- Temperature, humidity, RF environment (WiFi networks visible, Bluetooth devices)
- Surveillance cameras, witnesses, time of day
- Network infrastructure: Router, modem, ISP connection

### 2.3 Tool Preparation

**Hardware:**
- Faraday bags (multiple sizes, RF-shielded)
- Write blockers (USB, SATA, eMMC, UFS)
- Power supplies (portable battery packs, device-specific chargers)
- Forensic workstation (isolated network, write-protected storage)
- Camera (high-resolution, timestamped)
- Chain of custody forms, tamper-evident labels

**Software:**
- AIDA64 Android (latest version, verified signature)
- QPST/QFIL (latest version from Qualcomm developer portal)
- ADB (Android SDK platform-tools, verified checksum)
- Cellebrite UFED (latest version, license verified)
- Frida (latest version, verified signature)
- Hash verification tools (MD5, SHA-1, SHA-256)

---

## 3. ACQUISITION PROCEDURES

### 3.1 Faraday Bag Isolation

**Immediate Action:**
1. Place device in Faraday bag BEFORE any interaction
2. Seal bag with tamper-evident tape
3. Label with case number, date, time, handler initials
4. If device is ON and battery critical: connect charger through Faraday bag port (if available)
5. If no charging port: accept battery drain risk — do NOT open bag

**Rationale:** Prevents remote wipe commands, location tracking, and data exfiltration during transport and storage.

### 3.2 Write-Blocked Imaging

**For eMMC/UFS Storage:**
1. Connect write blocker between device and forensic workstation
2. Verify write blocker is functioning (read-only LED, no write activity)
3. Use Cellebrite UFED or FTK Imager to create bit-by-bit duplicate
4. Calculate hash (SHA-256) of original storage
5. Calculate hash of duplicate
6. Verify hash match
7. Work ONLY on duplicate for all subsequent analysis

**For SD Cards:**
1. Remove SD card from device (if accessible without power-on)
2. Connect to forensic workstation via write-blocked SD card reader
3. Image using dd or forensic tool
4. Calculate and verify hashes

**For SIM Cards:**
1. Remove SIM card from device (if accessible without power-on)
2. Connect to SIM card reader
3. Extract IMSI, ICCID, Ki (if possible), SMS, contacts
4. Document SIM cloning indicators (unusual SMS, call forwarding, network registration)

### 3.3 Live System Acquisition (If Device is ON)

**If legal authority permits live acquisition:**
1. Enable airplane mode (if safe — prevents remote commands but may alter volatile data)
2. Connect ADB via USB (if USB debugging is enabled)
3. Capture volatile data:
   - `adb shell ps` (running processes)
   - `adb shell netstat` (network connections)
   - `adb shell logcat -d` (system logs)
   - `adb shell dumpsys` (system service dumps)
4. Capture system properties:
   - `adb shell getprop` (all system properties — critical for DSU/GSI detection)
5. Capture partition information:
   - `adb shell cat /proc/partitions`
   - `adb shell mount`
   - `adb shell df`
6. Capture DSU status:
   - `adb shell gsi_tool list`
   - `adb shell gsi_tool status`
7. Capture baseband information:
   - `adb shell dumpsys telephony.registry`
   - `adb shell logcat -b radio -d`

**Rationale:** Volatile data (running processes, network connections, system logs) is lost when device is powered off. Live acquisition captures this data but may alter system state. Document all commands executed.

---

## 4. BASEBAND FORENSIC ANALYSIS

### 4.1 QXDM Diagnostic Interface Detection

**Using AIDA64 Android (Non-Destructive):**
1. Install AIDA64 Android from Google Play Store (verified developer: FinalWire Ltd.)
2. Navigate to: Directories → System → /dev
3. Search for: `ffs-diag`, `diag`, `diag_mdm`
4. Document: Device path, permissions, mount state, owner/group
5. Navigate to: Directories → System → /mnt
6. Search for: `rescue`, `qmcs`, `spunvm`
7. Document: Mount point, source partition, filesystem type, mount flags (read-only vs. read-write)

**Expected Results (Normal Device):**
- /dev/ffs-diag*: Not present or present with minimal permissions
- /mnt/rescue: Not mounted or mounted READ-ONLY
- /mnt/vendor/qmcs: Not mounted or mounted READ-ONLY
- /mnt/vendor/spunvm: Not mounted or mounted READ-ONLY

**Anomalous Results (Case RAK/CYB/2026/001):**
- /dev/ffs-diag: Present, READ-WRITE permissions
- /dev/ffs-diag-1: Present, READ-WRITE permissions (diag_mdm)
- /dev/ffs-diag-2: Present, READ-WRITE permissions (diag_mdm2)
- /mnt/rescue: Mounted, ext4, READ-WRITE
- /mnt/vendor/qmcs: Mounted, vfat, READ-WRITE
- /mnt/vendor/spunvm: Mounted, vfat, READ-WRITE

**Interpretation:** Any QXDM diagnostic interface on a consumer device is anomalous. READ-WRITE mount states on rescue and modem configuration partitions are highly suspicious. These findings indicate baseband-level compromise requiring further analysis.

### 4.2 QPST/QFIL Baseband Dump

**Prerequisites:**
- QPST/QFIL installed on Windows forensic workstation
- Qualcomm USB drivers installed
- Device in EDL (Emergency Download) mode or with ADB root access
- EDL mode: Power off device, hold Volume Up + Volume Down, connect USB

**QCN Backup (NV Items):**
1. Open QPST Configuration
2. Add new port: Device should appear as "Qualcomm HS-USB Diagnostic 900E" (or similar)
3. Open Software Download → Backup
4. Select QCN backup
5. Save to forensic storage with case number and timestamp
6. QCN file contains: IMEI, IMSI, network registration data, modem configuration, NV items

**NON-HLOS.bin Dump (Baseband Firmware):**
1. Open QFIL
2. Select "Flat Build"
3. Load programmer (prog_emmc_firehose_*.mbn for eMMC, prog_ufs_firehose_*.mbn for UFS)
4. Select "Read" tab
5. Select partition: modem, modemst1, modemst2, fsg, fsc
6. Dump to forensic storage with case number and timestamp
7. Calculate and record hash

**Interpretation:** Compare dumped firmware against known-good firmware for the device model. Any discrepancy indicates tampering. QCN analysis can reveal:
- Modified network registration parameters
- Unusual ARFCN values (rogue base station indicators)
- Modified IMEI/IMSI (cloning evidence)
- Unexpected diagnostic session logs

### 4.3 QXDM Log Analysis

**Using QXDM Professional (Qualcomm Diagnostic Monitor):**
1. Connect device via USB (QXDM interfaces must be active)
2. Open QXDM, select diagnostic port
3. Capture real-time logs:
   - Call Manager (CM) logs: Voice call events, SMS events
   - Location Manager (LM) logs: GPS coordinates, cell tower information
   - Data Services (DS) logs: Data connection events, IP addresses
   - System Identification (SYS) logs: Boot events, diagnostic session events
4. Save logs with timestamp and case number

**Interpretation:**
- Active diagnostic sessions without user initiation indicate unauthorized access
- GPS coordinates logged during device idle periods indicate tracking
- SMS interception events (message received but not delivered to OS) indicate baseband-level interception
- Unusual ARFCN values indicate rogue base station connection attempts

---

## 5. DSU/GSI FORENSIC ANALYSIS

### 5.1 DSU Status Detection

**Using ADB (Root or Standard):**
```bash
# List DSU slots
adb shell gsi_tool list

# Expected output (no DSU installed):
# No GSI installed

# Anomalous output (Case RAK/CYB/2026/001):
# DSU Image: gsi_gms_arm64
# DSU Image: gsi_arm64
# Status: installed

# Check DSU status
adb shell gsi_tool status

# Check dynamic partition state
adb shell lpdump

# List all partitions
adb shell cat /proc/partitions
```

**Interpretation:** Any DSU installation on a consumer device is anomalous. The presence of GSI images (especially Android 16 on an Android 14 device) indicates DSU exploitation. The `lpdump` output shows dynamic partition allocation — compare against factory image.

### 5.2 GSI Build Analysis

**Extract Build Properties:**
```bash
# Mount DSU partition (requires root)
adb shell su -c "mkdir /mnt/dsu"
adb shell su -c "mount /dev/block/dm-XX /mnt/dsu"  # XX = dynamic partition number

# Read build.prop
adb shell cat /mnt/dsu/system/build.prop

# Key properties to check:
# ro.build.version.release (Android version — e.g., 16 vs. 14)
# ro.build.id (build identifier)
# ro.build.type (user, userdebug, eng — userdebug/eng indicate test build)
# ro.build.tags (release-keys, test-keys — test-keys indicate unofficial)
# ro.build.fingerprint (full build identifier)
# ro.product.name (GSI vs. device-specific)
# ro.build.version.security_patch (security patch level)
```

**Interpretation:**
- Android version mismatch (16 on 14 device): Confirms version disparity
- BUILD_TYPE=userdebug or eng: Confirms test/debug build (not production)
- BUILD_TAGS=test-keys: Confirms unofficial/signed build
- Product name containing "gsi" or "aosp": Confirms GSI origin

### 5.3 Boot Partition Ramdisk Analysis

**Extract Boot Image:**
```bash
# Dump boot partition
adb shell su -c "dd if=/dev/block/bootdevice/by-name/boot of=/sdcard/boot.img"
adb pull /sdcard/boot.img

# Unpack boot image using Android Image Kitchen or magiskboot
# magiskboot unpack boot.img

# Analyze ramdisk:
# - Check for init.rc modifications (Magisk service startup)
# - Check for /sbin/.magisk directory (Magisk installation)
# - Check for post-fs-data.sh (Magisk boot script)
# - Check for LSPosed module initialization
```

**Interpretation:**
- Presence of Magisk files in ramdisk: Confirms root modification
- LSPosed module references: Confirms Zygote hooking framework
- Modified init.rc: Confirms boot-time service injection
- Any modification to boot ramdisk indicates persistent root that survives OS replacement

### 5.4 Rescue Partition Analysis

**Extract and Hash Rescue Partition:**
```bash
# Dump rescue partition
adb shell su -c "dd if=/dev/block/bootdevice/by-name/rescue of=/sdcard/rescue.img"
adb pull /sdcard/rescue.img

# Calculate hash
sha256sum rescue.img

# Compare against known-good hash from manufacturer
# Known-good hash for Xiaomi 11T Pro (vili) HyperOS 14.x: [obtain from Xiaomi firmware repository]
```

**Interpretation:**
- Hash mismatch: Confirms rescue partition tampering
- File-level analysis: Examine modified files for malicious scripts, backdoor entries, or modified recovery procedures
- Any modification to rescue partition indicates factory reset survival mechanism

---

## 6. OS-LEVEL FORENSIC ANALYSIS

### 6.1 System Property Audit

**Dump All Properties:**
```bash
adb shell getprop > device_properties.txt
```

**Key Properties to Analyze:**

| Property | Normal Value | Anomalous Value | Indication |
|----------|-------------|-----------------|------------|
| ro.build.type | user | userdebug, eng | Debug/test build |
| ro.build.tags | release-keys | test-keys | Unofficial signing |
| ro.debuggable | 0 | 1 | Debug mode enabled |
| ro.secure | 1 | 0 | ADB root enabled |
| ro.treble.enabled | true | false | Treble disabled (GSI requirement) |
| ro.build.version.release | 14 | 16 | Version disparity (GSI) |
| ro.product.name | vili | gsi_arm64 | GSI product name |
| ro.build.fingerprint | Xiaomi/vili/... | aosp/gsi/... | GSI fingerprint |
| ro.boot.verifiedbootstate | green | yellow, orange | Boot verification failed |
| ro.boot.vbmeta.device_state | locked | unlocked | Bootloader unlocked |

**Interpretation:** Any anomalous value indicates system modification. Multiple anomalies (debuggable=1, secure=0, build type=userdebug) strongly indicate persistent root and test build environment.

### 6.2 Application Analysis

**List All Applications:**
```bash
adb shell pm list packages -f > all_apps.txt
adb shell pm list packages -s > system_apps.txt
adb shell pm list packages -3 > user_apps.txt
```

**Check for Modified/System Apps:**
```bash
# Check app signatures
adb shell pm dump com.whatsapp | grep signature

# Check for debug builds
adb shell pm dump com.whatsapp | grep flags

# Look for:
# - DEBUGGABLE flag
# - TEST_ONLY flag
# - Modified signature (not matching official WhatsApp signature)
```

**Interpretation:** Modified signatures or debug flags on system apps (WhatsApp, Google Play Services) indicate tampered APK installation. This is consistent with the "modified WhatsApp APK with backdoor entry points" finding in Chapter 1.

### 6.3 Network Configuration Analysis

**Dump Network Configuration:**
```bash
adb shell netcfg
adb shell ip route
adb shell ip rule
adb shell dumpsys connectivity
adb shell dumpsys wifi
```

**Check for VPN Profiles:**
```bash
adb shell dumpsys connectivity | grep -i vpn
adb shell settings list global | grep vpn
```

**Interpretation:** Active VPN profiles, unusual routing rules, or persistent VPN connections may indicate C2 channel infrastructure. Compare against user's known VPN usage.

---

## 7. REPORTING AND PRESENTATION

### 7.1 Forensic Report Structure

**Executive Summary:**
- Case reference, date, examiner credentials
- Device identification (model, serial, IMEI, software version)
- Summary of findings (compromise confirmed/possible/unlikely)
- Key evidence items (clone count, DSU status, baseband anomalies)

**Methodology:**
- Tools used (versions, licenses, verification)
- Procedures followed (acquisition, analysis, documentation)
- Chain of custody (who handled, when, where, why)
- Limitations (what could not be analyzed, why)

**Findings:**
- Chronological presentation of evidence
- Technical details with screenshots, command outputs, logs
- Interpretation of findings (what they mean, how they were determined)
- Correlation with attack timeline (when each finding was likely introduced)

**Conclusions:**
- Overall assessment of compromise (confirmed, probable, possible, unlikely)
- Confidence level for each finding
- Recommendations for further analysis
- Recommendations for remediation

**Appendices:**
- Raw data dumps (hashed, verified)
- Tool output logs
- Photographs and screenshots
- Expert witness qualifications

### 7.2 Expert Witness Preparation

**Qualifications Documentation:**
- Certifications: EnCE, GCFE, GCFA, CCFE, or equivalent
- Training: Cellebrite, XRY, QPST, or manufacturer-specific courses
- Experience: Number of cases, types of devices, courtroom testimony history
- Publications: Papers, presentations, training materials
- Continuing education: Recent training, conference attendance, certification maintenance

**Mock Cross-Examination Preparation:**
- Anticipate challenges: chain of custody gaps, tool reliability, alternative explanations, examiner bias
- Practice explaining technical concepts in plain language
- Prepare visual aids: timelines, diagrams, screenshots, flowcharts
- Rehearse responses to "How do you know...?" questions
- Acknowledge limitations transparently

**Courtroom Presentation:**
- Dress professionally, arrive early, bring organized materials
- Speak clearly, make eye contact with jury/judge
- Use visual aids to illustrate complex concepts
- Avoid jargon; explain every technical term
- Stay within scope of expertise; defer to other experts when appropriate
- Maintain composure under aggressive questioning

---

## 8. CONCLUSION

The forensic investigation of Case RAK/CYB/2026/001 required techniques beyond standard mobile forensic practice. The DSU/GSI multi-environment infrastructure and baseband-level diagnostic exploitation documented in Chapter 1 are not detectable by Cellebrite UFED, GrayKey, or XRY alone. Specialized tools — AIDA64 Android, QPST/QFIL, ADB, and Frida — were essential for complete analysis.

The key forensic principles for this case class are:
1. **Standard tools are insufficient** — specialized baseband and DSU analysis is required
2. **Live acquisition is essential** — volatile data (running processes, network connections) is lost on power-off
3. **Baseband is below the OS** — no Android security tool can detect QXDM exploitation
4. **DSU is outside the primary OS** — standard forensic extraction misses GSI environments entirely
5. **Chain of custody is critical** — every step must be documented for legal admissibility
6. **Expert witness preparation is make-or-break** — technical findings must be presented accessibly and credibly

The techniques documented in this chapter are not theoretical. They were applied to the actual device in Case RAK/CYB/2026/001 and produced the findings presented in Chapter 1. They are applicable to any Treble-compliant Qualcomm device and should be incorporated into standard mobile forensic training curricula.

As the Android ecosystem continues to evolve — with DSU, GSI, AVF, and baseband diagnostic interfaces becoming more complex — the gap between attacker capabilities and forensic detection will widen. The security community must invest in specialized training, tool development, and methodology research to maintain parity.

---

**End of Chapter 4**
**Next Chapter:** Chapter 5 — Victim Support and Psychological Recovery (if required)
