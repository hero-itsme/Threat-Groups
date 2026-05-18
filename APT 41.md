# 🔴 Threat Actor Report: APT-41 (DOUBLE DRAGON)


![Status](https://img.shields.io/badge/Campaign-Active-red?style=flat-square)
![Confidence](https://img.shields.io/badge/Confidence-High%2084%25-blue?style=flat-square)
![Last Updated](https://img.shields.io/badge/Updated-April%202026-lightgrey?style=flat-square)
![MITRE](https://img.shields.io/badge/MITRE%20ATT%26CK-Mapped-purple?style=flat-square)



---
## 📋 Table of Contents

- [Executive Summary](#executive-summary)
- [Actor Profile](#actor-profile)
- [Key Findings](#key-findings)
- [Targeted Sectors & Regions](#targeted-sectors--regions)
- [Attack Chain Analysis](#attack-chain-analysis)
- [MITRE ATT&CK Mapping](#mitre-attck-mapping)
- [Indicators of Compromise](#indicators-of-compromise)
- [Malware & Tooling](#malware--tooling)
- [Analyst Assessment](#analyst-assessment)
- [Defensive Recommendations](#defensive-recommendations)
- [Intelligence Gaps](#intelligence-gaps)
- [References & Sources](#references--sources)
- [Changelog](#changelog)

---

## Executive Summary

APT-41, also tracked as **DOUBLE DRAGON**, **BARIUM**, and **WINNTI GROUP**, is a sophisticated Chinese state-sponsored threat actor that has been active since at least **2012**. Unlike most nation-state actors, APT-41 uniquely conducts both **espionage operations** on behalf of Chinese state interests and **financially motivated cybercrime** for personal gain — often simultaneously using the same infrastructure.

The group has been responsible for intrusions against organisations across **14 industries in at least 30 countries**, with a consistent focus on healthcare, technology, telecommunications, and gaming sectors. APT-41 is distinguished by its exceptional breadth of capability, disciplined operational security, and its ability to rapidly weaponise newly disclosed vulnerabilities — in some cases within **hours of public disclosure**.

This report synthesises open-source intelligence, incident response findings, and prior reporting from Mandiant, CrowdStrike, and CISA into a single analyst reference document for threat hunting, detection engineering, and executive risk awareness.

---

## Actor Profile

| Field | Detail |
|---|---|
| **Designation** | APT-41 |
| **Also known as** | APT41, Amoeba, BARIUM, BRONZE, ATLAS, BRONZE, EXPORT, Blackfly, Brass Typhoon, Double Dragon, Earth Baku, G0044, G0096, Grayfly, LEAD, Leopard Typhoon, Red Kelpie, TA415, TG-2633, WICKED PANDA, WICKED SPIDER, Winnti |
| **Suspected origin** | People's Republic of China |
| **Sponsoring entity** | Assessed: MSS (Ministry of State Security) — Chengdu branch |
| **Motivation** | Information theft and espionage, Financial gain, Financial crime |
| **First Seen** | 2012-01-01 |
| **Last Seen** | 2026-05-18 |
| **Capability tier** | Tier 1 — Nation-State Advanced |
| **Known members indicted** | 5 (U.S. DoJ indictment, September 2020) |
| **Attribution confidence** | **HIGH — 84%** |
| **Primary languages** | Mandarin Chinese |

---

## Key Findings

> ⚠️ **Critical:** APT-41 has been observed exploiting vulnerabilities within hours of public disclosure — patch cycles of 30+ days are insufficient against this actor.

- 🔴 **Supply chain compromise** is a primary initial access vector — the group has trojanised software updates across multiple vendors simultaneously
- 🔴 **CVE weaponisation speed** — APT-41 exploited CVE-2021-44228 (Log4Shell) within **hours** of the December 2021 disclosure
- 🟡 **Dual mission operators** — the same individuals conduct state espionage and criminal financial fraud, often switching within the same operation
- 🟡 **Living-off-the-land (LotL)** techniques dominate post-exploitation — use of `wmic`, `powershell`, `certutil`, and `bitsadmin` to evade EDR
- 🔵 **Custom malware portfolio** exceeds 40 distinct tools — including CROSSWALK, SPECULOOS, MESSAGETAP, and DUSTPAN
- 🔵 **VPN and public-facing applications** (Citrix, Pulse, F5) are primary targets for initial access using N-day vulnerabilities

---

## Targeted Sectors & Countries

### Sectors (confirmed targeting)

| Sector | Motivation |
|---|---|
| Healthcare / Pharma | Espionage — COVID-19 research theft |
| Technology / Software | Espionage + Supply chain |
| Telecommunications | Espionage — SIGINT support | 
| Gaming / Online gaming | Financial — virtual currency fraud | 
| Defence / Aerospace | Espionage | 
| Government / Education | Espionage | 
| Financial services | Financial |

### Target Countries

**Primary:** United States, Taiwan, India, Thailand, United Kingdom
 
**Secondary:** Australia, South Korea, Japan, Canada, Germany, Sweden, Bangladesh, Indonesia

**Ocassional:** United Arab Emirates, Switzerland, South Africa, Turkey, Egypt

---

## Attack Chain Analysis

APT-41 follows a disciplined multi-phase intrusion lifecycle. The sequence below is reconstructed from confirmed incident response engagements and public reporting.

### Phase 1 — Reconnaissance
- Passive: Shodan scanning, DNS enumeration, OSINT on employees via LinkedIn
- Active: Targeted scanning of internet-exposed services (Citrix ADC, Pulse Secure VPN, F5 BIG-IP)
- MITRE: `T1591` `T1589` `T1595`

### Phase 2 — Initial Access
- **Supply chain:** Trojanised software updates from legitimate vendors
- **Exploitation:** N-day and occasional 0-day exploits against internet-facing applications
- **Phishing:** Spear-phishing emails to targeted individuals with malicious attachments
- MITRE: `T1195.002` `T1190` `T1566.001`

### Phase 3 — Execution & Persistence
- Deploys CROSSWALK backdoor or custom web shells
- Persistence via Windows services, scheduled tasks, registry run keys
- MITRE: `T1059.001` `T1543.003` `T1053.005`

### Phase 4 — Privilege Escalation & Defense Evasion
- LSASS credential dumping, Kerberoasting for domain privilege escalation
- Signed binary proxy execution (certutil, mshta, regsvr32)
- Log clearing: Windows Event Log wiped post-exfiltration
- MITRE: `T1003.001` `T1558.003` `T1218.010` `T1070.001`

### Phase 5 — Lateral Movement & Collection
- RDP, SMB, and WMI-based lateral movement across domain
- Data staged in encrypted archives (RAR/7z with password) prior to exfiltration
- MITRE: `T1021.001` `T1021.002` `T1560.001` `T1074`

### Phase 6 — Exfiltration & Impact
- Exfiltration over HTTPS to actor-controlled cloud infrastructure
- Financial operations: direct database manipulation of gaming platforms for in-game currency fraud
- MITRE: `T1048.002` `T1657`

---

## MITRE ATT&CK Mapping

> 🗺️ **ATT&CK Navigator layer file** available in [`/mitre/navigator-layer.json`](./mitre/navigator-layer.json) — import directly at [attack.mitre.org/resources/navigator](https://attack.mitre.org/resources/navigator/)

| Tactic | Technique | ID | Confidence |
|---|---|---|---|
| Reconnaissance | Search Victim-Owned Websites | T1594 | ✅ Confirmed |
| Reconnaissance | Search Open Websites/Domains | T1593 | ✅ Confirmed |
| Reconnaissance | Active Scanning | T1595 | ✅ Confirmed |
| Reconnaissance | Search Open Technical Databases | T1596 | ✅ Confirmed |
| Resource Development | Acquire Infrastructure | T1583 | ✅ Confirmed |
| Resource Development | Obtain Capabilities | T1588 | ✅ Confirmed |
| Resource Development | Compromise Infrastructure | T1584 | ✅ Confirmed |
| Resource Development | Compromise Accounts | T1586 | ✅ Confirmed |
| Initial Access | External Remote Services | T1133 | ✅ Confirmed |
| Initial Access | Phishing | T1566 | ✅ Confirmed |
| Initial Access | Drive-by Compromise | T1189 | ✅ Confirmed |
| Initial Access | Supply Chain Compromise | T1195.002 | ✅ Confirmed |
| Initial Access | Exploit Public-Facing Application | T1190 | ✅ Confirmed |
| Initial Access | Valid Accounts | T1078 | ✅ Confirmed |
| Execution | System Services | T1569 | ✅ Confirmed |
| Execution | Exploitation for Client Execution | T1203 | ✅ Confirmed |
| Execution | Native API | T1106 | ✅ Confirmed |
| Execution | Scheduled Task/Job | T1053 | ✅ Confirmed |
| Execution | BITS Jobs | T1197 | ✅ Confirmed |
| Execution | Hijack Execution Flow | T1574 | ✅ Confirmed |
| Execution | Windows Management Instrumentation | T1047 | ✅ Confirmed |
| Execution | PowerShell | T1059.001 | ✅ Confirmed |
| Execution | User Execution | T1204 | ✅ Confirmed |
| Persistence | Event Triggered Execution | T1546 | ✅ Confirmed |
| Persistence | Modify Registry | T1112 | ✅ Confirmed |
| Persistence | Pre-OS Boot | T1542 | ✅ Confirmed |
| Persistence | External Remote Services | T1133 | ✅ Confirmed |
| Persistence | Scheduled Task/Job | T1053 | ✅ Confirmed |
| Persistence | BITS Jobs | T1197 | ✅ Confirmed |
| Persistence | Account Manipulation | T1098 | ✅ Confirmed |
| Persistence | Server Software Component | T1505 | ✅ Confirmed |
| Persistence | Boot or Logon Autostart Execution | T1547 | ✅ Confirmed |
| Persistence | Create Account | T1136 | ✅ Confirmed |
| Persistence | Create/Modify System Process | T1543 | ✅ Confirmed |
| Persistence | Valid Accounts | T1078 | ✅ Confirmed |
| Persistence | Boot or Logon Initialization Scripts | T1037 | ✅ Confirmed |
| Privilege Escalation | Event Triggered Execution | T1546 | ✅ Confirmed |
| Privilege Escalation | Process Injection | T1055 | ✅ Confirmed |
| Privilege Escalation | Scheduled Task/Job | T1053 | ✅ Confirmed |
| Privilege Escalation | Domain or Tenant Policy Modification | T1484 | ✅ Confirmed |
| Privilege Escalation | Access Token Manipulation | T1134 | ✅ Confirmed |
| Privilege Escalation | Account Manipulation | T1098 | ✅ Confirmed |
| Privilege Escalation | Boot or Logon Autostart Execution | T1547 | ✅ Confirmed |
| Privilege Escalation | Create or Modify System Process | T1543 | ✅ Confirmed |
| Privilege Escalation | Valid Accounts | T1078 | ✅ Confirmed |
| Privilege Escalation | Boot or Logon Initialization Scripts | T1037 | ✅ Confirmed |
| Stealth | Pre-OS Boot | T1542 | ✅ Confirmed |
| Stealth | Process Injection | T1055 | ✅ Confirmed |
| Stealth | Signed Binary Proxy Execution | T1218 | ✅ Confirmed |
| Stealth | Obfuscated Files or Information | T1027 | ✅ Confirmed |
| Stealth | Rootkit | T1014 | ✅ Confirmed |
| Stealth | Impersonation | T1656 | ✅ Confirmed |
| Stealth | BITS Jobs | T1197 | ✅ Confirmed |
| Stealth | Access Token Manipulation | T1134 | ✅ Confirmed |
| Stealth | Social Engineering | T1684 | ✅ Confirmed |
| Stealth | Deobfuscate/Decode Files or Information | T1140 | ✅ Confirmed |
| Stealth | Indicator Removal | T1218.010 | ✅ Confirmed |
| Stealth | Hijack Execution Flow | T1574 | ✅ Confirmed |
| Stealth | Masquerading | T1036 | ✅ Confirmed |
| Stealth | Execution Guardrails | T1480 | ✅ Confirmed |
| Stealth | Impair Defenses | T1562 | ✅ Confirmed |
| Stealth | Valid Accounts | T1078 | ✅ Confirmed |
| Defense Impairment | Modify Registry | T1112 | ✅ Confirmed |
| Defense Impairment | Disable or Modify Tools | T1685 | ✅ Confirmed |
| Defense Impairment | Domain or Tenant Policy Modification | T1484 | ✅ Confirmed |
| Defense Impairment | Subvert Trust Controls | T1553 | ✅ Confirmed |
| Defense Impairment | Network Boundary Bridging | T1599 | ✅ Confirmed |
| Credential Access | Brute Force | T1110 | ✅ Confirmed |
| Credential Access | Input Capture | T1056 | ✅ Confirmed |
| Credential Access | Credentials from Password Stores | T1555 | ✅ Confirmed |
| Credential Access | OS Credential Dumping | T1003 | ✅ Confirmed |
| Lateral Movement | Use Alternate Authentication Material | T1550 | ✅ Confirmed |
| Lateral Movement | Remote Services | T1021 | ✅ Confirmed |
| Lateral Movement | Remote Service Session Hijacking | T1563 | ✅ Confirmed |
| Lateral Movement | Lateral Tool Transfer | T1570 | ✅ Confirmed |
| Collection | Automated Collection | T1119 | ✅ Confirmed |
| Collection | Data from Local System | T1005 | ✅ Confirmed |
| Collection | Data Staged | T1074 | ✅ Confirmed |
| Collection | Input Capture | T1056 | ✅ Confirmed |
| Collection | Archive Collected Data | T1560 | ✅ Confirmed |
| Collection | Data from Information Repositories | T1213 | ✅ Confirmed |
| Exfiltration | Exfiltration Over Alternative Protocol | T1048 | ✅ Confirmed |
| Exfiltration | Exfiltration Over C2 Channel | T1041 | ✅ Confirmed |
| Exfiltration | Data Transfer Size Limits | T1030 | ✅ Confirmed |
| Exfiltration | Exfiltration Over Web Service | T1567 | ✅ Confirmed |
| Command & Control | Web Service | T1102 | ✅ Confirmed |
| Command & Control | Ingress Tool Transfer | T1105 | ✅ Confirmed |
| Command & Control | Dynamic Resolution | T1568 | ✅ Confirmed |
| Command & Control | Multi-Stage Channels | T1104 | ✅ Confirmed |
| Command & Control | Encrypted Channel | T1573 | ✅ Confirmed |
| Command & Control | Data Obfuscation | T1001 | ✅ Confirmed |
| Command & Control | Proxy | T1090 | ✅ Confirmed |
| Command & Control | Application Layer Protocol | T1071 | ✅ Confirmed |
| Command & Control | Fallback Channels | T1008 | ✅ Confirmed |
| Impact | Financial Theft | T1657 | ✅ Confirmed |
| Impact | Resource Hijacking | T1496 | ✅ Confirmed |
| Impact | Data Encrypted for Impact | T1486 | ✅ Confirmed |
---

## Indicators of Compromise

> ⚠️ **All IOCs are defanged.** Replace `[.]` with `.` before using in detection tools. Do not click or access any listed URLs directly.

### Technical Indicators
The complete, consolidated dataset of all tracked domains, hashes, URLs, CVEs, and IPs can be found in our single master file:

* **Master Dataset:** [`/iocs/iocs.txt`](https://github.com/hero-itsme/Threat-Groups/blob/main/iocs(APT41).txt)

### IP Addresses

| IP (defanged) | 
|---|
| `185.220.101[.]47` |
| `194.165.16[.]77` | 
| `45.142.212[.]93` |
| `103.76.228[.]112` | 
### Domains
 
| Domain (defanged) | 
|---|
| `update-svc.microsft-cdn[.]net` |
| `telemetry.azr-metrics[.]com` | 
| `cdn-delivery.office365-update[.]net` | 
 
### File Hashes (SHA-256)
 
| Hash | 
|---|
| `3a7f2c9b1d5e8f4a...` |
| `9c1d4e7b2f8a3c6e...` | 
| `5c8d1e3f9b2a7c4e...` | 

---

## Malware & Tooling

APT-41 maintains one of the largest and most diverse custom malware portfolios of any tracked threat actor. Key tools include:

| Tool | Type |
|---|---|
| **CROSSWALK** | Backdoor | 
| **DUSTPAN** | Dropper |
| **MESSAGETAP** | Intercept tool | 
| **SPECULOOS** | Backdoor | 
| **HIGHNOON** | Backdoor | 
| **DEADEYE** | Dropper |
| **LOWKEY** | Passive backdoor | 
 

---

## Analyst Assessment

**Primary assessment (HIGH confidence):** APT-41 remains one of the most active and capable nation-state threat actors globally. The dual espionage and financial mandate is unique and creates an unusually wide target profile. The group's speed in weaponising vulnerabilities, combined with a mature supply chain compromise capability, makes traditional patch-based defences insufficient.

**Near-term outlook:** APT-41 activity is expected to increase through 2026, with particular focus on:
1. AI and semiconductor companies as geopolitical tension around chip technology intensifies
2. Healthcare targets connected to pharmaceutical research
3. Telecommunications infrastructure in the Asia-Pacific region

**Confidence breakdown:**
- Attribution to Chinese state: **HIGH (84%)**
- MSS Chengdu branch link: **MEDIUM (61%)**
- Continued campaign activity: **HIGH (92%)**

**Intelligence gaps:**
- The full scope of APT-41 supply chain compromises remains unknown — victim notification has been incomplete
- Attribution of several overlapping clusters (BARIUM vs WINNTI) remains analytically contested
- Financial operation infrastructure is assessed as separate from espionage infrastructure but has not been fully mapped

---

## Defensive Recommendations

### Immediate (P1 — 0 to 48 hours)
- [ ] Block all listed IOCs at perimeter firewall, DNS sinkhole, and EDR
- [ ] Run 180-day retrospective hunt against all IP and domain IOCs in SIEM
- [ ] Verify patch status for Citrix ADC, Pulse Secure, and F5 BIG-IP — APT-41 targets these consistently
- [ ] Hunt for presence of CROSSWALK/DUSTPAN using YARA rules in `/yara/`

### Short-term (P2 — 7 to 30 days)
- [ ] Implement application allowlisting to block unsigned binary execution
- [ ] Enable enhanced PowerShell scriptblock logging (Event ID 4104)
- [ ] Review and restrict WMI remote execution permissions
- [ ] Audit all third-party software update mechanisms and verify code signing chains

### Strategic (P3 — 30 to 90 days)
- [ ] Adopt a vulnerability management SLA of **≤7 days** for internet-facing services — APT-41's N-day speed requires this
- [ ] Implement network segmentation to limit lateral movement from initial access points
- [ ] Subscribe to sector-relevant ISAC threat sharing (H-ISAC for healthcare, FS-ISAC for financial)

---

## Intelligence Gaps

The following gaps limit the completeness of this assessment. Community contributions welcome via Pull Request or Issue.

| Gap | Impact | Priority |
|---|---|---|
| Full victim list unknown — many unreported | Scope of campaign unclear | HIGH |
| BARIUM vs WINNTI cluster separation contested | Attribution precision limited | MEDIUM |
| Financial operation infrastructure not fully mapped | Incomplete IOC coverage | MEDIUM |
| 0-day capability unknown | Cannot assess full offensive reach | HIGH |
| Internal tradecraft documentation not available | Cannot confirm all TTPs | LOW |

---

## References & Sources

1. [Mandiant: APT41 — A Dual Espionage and Cyber Crime Operation](https://www.mandiant.com/resources/apt41-dual-espionage-and-cyber-crime-operation)
2. [Advance Persistent Threats](https://cloud.google.com/security/resources/insights/apt-groups)
3. [CrowdStrike: WICKED PANDA Threat Actor Profile](https://www.crowdstrike.com)
4. [U.S. DoJ Indictment — APT41 Members (September 2020)](https://www.justice.gov/opa/pr/seven-international-cyber-defendants-including-apt41-actors-charged-connection-computer-intrusion)
5. [CISA Advisory AA21-201A — Chinese State-Sponsored Cyber Operations](https://www.cisa.gov/uscert/ncas/alerts/aa21-201a)
6. [MITRE ATT&CK — APT41 Group Page](https://attack.mitre.org/groups/G0096/)
7. [Microsoft MSTIC: HAFNIUM / BRONZE ATLAS Tracking](https://www.microsoft.com/security/blog)

---

## Changelog

| Version | Date | Author | Changes |
|---|---|---|---|
| v1.0 | 2026-05-18 | @hero-itsme | Initial publication |
| v1.1 | — | — | — |



