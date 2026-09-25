# FIN7 (G0046) — Cyber Threat Intelligence Analysis

**Report ID:** CTI-2026-09-23-APT
**Date:** 23 September 2026
**Priority:** High
**TLP:** CLEAR
**Source & Information Reliability:** A-1

---

## 1. Executive Summary

**FIN7**, tracked by MITRE ATT&CK as **G0046**, is a financially motivated cybercriminal group active since at least 2013.

Known aliases include:

* Carbon Spider
* GOLD NIAGARA
* ELBRUS
* ITG14
* Sangria Tempest

FIN7 has historically been associated with the theft of payment-card data, particularly from retail, restaurant and hospitality organizations.

Its documented activity has expanded toward:

* Enterprise intrusion
* Data theft
* Initial-access operations
* Custom malware and loaders
* Ransomware-related activity
* Financial extortion

The research indicates that FIN7 has adapted its tooling and operational procedures over time. Documented malware and tooling includes **POWERPLANT, BIRDWATCH, LOADOUT, GRIFFON, POWERTRASH, CARBANAK and DICELOADER**.

Historical malware signatures and static indicators alone may therefore provide limited coverage against changing FIN7 operations.

---

# 2. Threat Actor Profile

| Attribute              | Details                                                                                                                          |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Threat Actor           | FIN7                                                                                                                             |
| MITRE ATT&CK ID        | G0046                                                                                                                            |
| Motivation             | Cybercrime / Financial gain                                                                                                      |
| Activity               | Enterprise intrusion, data theft, ransomware & extortion                                                                         |
| Aliases                | Carbon Spider, GOLD NIAGARA, ELBRUS, ITG14, Sangria Tempest                                                                      |
| Historical Focus       | Payment-card theft                                                                                                               |
| Geographic Victimology | North America and Europe prominently represented                                                                                 |
| Sectors                | Retail, hospitality, financial services, software, technology, healthcare, transportation, utilities, pharmaceuticals and others |

---

# 3. Intelligence Sources

The report uses publicly available threat-intelligence research from:

* MITRE ATT&CK
* Blackpoint Cyber / Adversary Pursuit Group
* Google Cloud / Mandiant
* PRODAFT

The research is primarily based on OSINT and publicly documented threat research.

---

# 4. Cyber Kill Chain Analysis

## 4.1 Reconnaissance

FIN7 has conducted victim research and selection.

Documented activity includes gathering information about targeted organizations, employees and IT personnel with elevated privileges.

**MITRE ATT&CK:**

* T1591 — Gather Victim Organization Information
* T1591.004 — Gather Victim Organization Information: Identify Roles

---

## 4.2 Weaponization

FIN7 has developed or obtained malware and supporting tooling.

Documented capabilities include:

* CARBANAK
* BIRDWATCH
* POWERPLANT
* DICELOADER
* STONEBOAT
* BOOSTWRITE
* PowerShell tooling
* Cobalt Strike

FIN7 has also been documented using trojanized legitimate software and cloud infrastructure for malicious payload delivery.

---

## 4.3 Delivery

Documented delivery methods include:

* Spearphishing attachments
* Malicious links
* Trojanized software
* Compromised websites
* Supply-chain compromise
* Malicious USB devices
* Compromised email/marketing platforms

---

## 4.4 Exploitation

FIN7 has exploited:

* Public-facing applications
* Remote services
* Vulnerable enterprise applications
* Malicious documents
* PowerShell
* Windows Management Instrumentation

Documented vulnerabilities include:

* **CVE-2021-31207**
* **CVE-2020-1472 (ZeroLogon)**

---

## 4.5 Installation & Persistence

Documented persistence mechanisms include:

* Scheduled Tasks
* Registry Run/RunOnce keys
* Windows services
* Application shimming
* OpenSSH
* Masquerading
* Hidden files and directories

One documented scheduled task is:

```text
AdobeFlashSync
```

---

## 4.6 Command & Control

FIN7 has used:

* HTTP/HTTPS
* DNS
* Legitimate web services
* Remote-access infrastructure
* Non-standard ports
* OpenSSH tunneling

Documented techniques include:

* T1071.001 — Web Protocols
* T1071.004 — DNS
* T1105 — Ingress Tool Transfer
* T1090 — Proxy
* T1572 — Protocol Tunneling
* T1102 — Web Service

---

## 4.7 Actions on Objectives

Documented objectives include:

* Payment-card theft
* Credential theft
* Data collection
* Data exfiltration
* Financial theft
* Ransomware
* Extortion

Collection and exfiltration behaviors include file collection, screen capture, audio capture and transfer of data through cloud-storage services such as MEGA.

---

# 5. Indicators of Compromise

## 5.1 Endpoint Artifacts

Examples documented in the research include:

```text
3CF9.ps1
WsTaskLoad.exe
AdobeFlashSync
net group "Domain Admins" /domain
tasklist /v
cmd.exe /C quser
sc start sshd
certutil -decode hex
```

Additional artifacts include:

```text
TCP 59999
TCP 9898
C:\ProgramData\ssh
qawsed1q2w3e
```

---

## 5.2 Network Indicators

Documented domains include:

```text
advanced-ip-sccanner[.]com
softowii[.]com
mozillaupdate[.]com
milkmovemoney[.]com
tableofcolorize[.]com
moviedvdpower[.]com
landscapesboxdesign9[.]com
hawrickday[.]com
colormiagi[.]com
```

Documented IP addresses include:

```text
45.11.180.82
138.124.180.226
185.172.129.144
37.252.4.131
45.133.216.25
45.140.146.184
184.95.57.98
45.147.228.239
206.166.251.200
94.158.244.91
94.158.244.18
```

The report also documents historical TOR infrastructure.

> **IOC handling note:** These indicators are historical/publicly reported intelligence and should be validated before operational use.

---

# 6. Malware & Tooling

The report identifies the following malware and tools:

| Malware / Tool           |
| ------------------------ |
| CARBANAK                 |
| BOOSTWRITE               |
| Cobalt Strike            |
| AdFind                   |
| PowerSploit / POWERTRASH |
| Lizar                    |
| JSS Loader               |
| Harpy                    |
| DICELOADER               |
| STONEBOAT                |
| Atera                    |

---

# 7. Vulnerability Intelligence

| CVE                       | CVSS | Patch Available |
| ------------------------- | ---: | --------------- |
| CVE-2021-31207            |  9.8 | Yes             |
| CVE-2020-1472 (ZeroLogon) | 10.0 | Yes             |

The report records these vulnerabilities in the context of documented FIN7 exploitation activity.

---

# 8. MITRE ATT&CK Mapping

## Reconnaissance

| Technique | Name                                   |
| --------- | -------------------------------------- |
| T1591     | Gather Victim Organization Information |
| T1591.004 | Identify Roles                         |

## Resource Development

| Technique | Name                               |
| --------- | ---------------------------------- |
| T1583.001 | Acquire Infrastructure: Domains    |
| T1584.001 | Compromise Infrastructure: Domains |
| T1585.002 | Establish Accounts: Email Accounts |

## Initial Access

| Technique | Name                                           |
| --------- | ---------------------------------------------- |
| T1566.001 | Phishing: Spearphishing Attachment             |
| T1566.002 | Phishing: Spearphishing Link                   |
| T1190     | Exploit Public-Facing Application              |
| T1189     | Drive-by Compromise                            |
| T1199     | Trusted Relationship                           |
| T1195.002 | Supply Chain Compromise: Software Supply Chain |

## Execution

| Technique | Name                               |
| --------- | ---------------------------------- |
| T1059.001 | PowerShell                         |
| T1059.003 | Windows Command Shell              |
| T1059.005 | Visual Basic                       |
| T1059.007 | JavaScript/JScript                 |
| T1204.002 | User Execution: Malicious File     |
| T1047     | Windows Management Instrumentation |

## Persistence

| Technique | Name                               |
| --------- | ---------------------------------- |
| T1053.005 | Scheduled Task/Job                 |
| T1547.001 | Registry Run Keys / Startup Folder |
| T1543.003 | Windows Service                    |
| T1546.001 | Change Default File Association    |
| T1546.013 | PowerShell Profile                 |

## Privilege Escalation

| Technique | Name                                  |
| --------- | ------------------------------------- |
| T1068     | Exploitation for Privilege Escalation |
| T1548     | Abuse Elevation Control Mechanism     |

## Defense Evasion

| Technique | Name                                         |
| --------- | -------------------------------------------- |
| T1027     | Obfuscated/Compressed Files and Information  |
| T1036     | Masquerading                                 |
| T1070.004 | File and Directory Discovery / File Deletion |
| T1562.001 | Impair Defenses: Disable or Modify Tools     |

## Credential Access

| Technique | Name                  |
| --------- | --------------------- |
| T1003     | OS Credential Dumping |
| T1558.003 | Kerberoasting         |
| T1078     | Valid Accounts        |

## Discovery

| Technique | Name                                   |
| --------- | -------------------------------------- |
| T1057     | Process Discovery                      |
| T1087.002 | Domain Account Discovery               |
| T1069.002 | Domain Groups Discovery                |
| T1049     | System Network Connections Discovery   |
| T1016     | System Network Configuration Discovery |
| T1033     | System Owner/User Discovery            |

## Lateral Movement

| Technique | Name                 |
| --------- | -------------------- |
| T1021.001 | Remote Services: RDP |
| T1021.004 | Remote Services: SSH |
| T1021.005 | Remote Services: VNC |
| T1078     | Valid Accounts       |

## Command & Control

| Technique | Name                  |
| --------- | --------------------- |
| T1071.001 | Web Protocols         |
| T1071.004 | DNS                   |
| T1105     | Ingress Tool Transfer |
| T1090     | Proxy                 |
| T1572     | Protocol Tunneling    |
| T1102     | Web Service           |

## Collection

| Technique | Name                   |
| --------- | ---------------------- |
| T1005     | Data from Local System |
| T1113     | Screen Capture         |
| T1123     | Audio Capture          |

## Exfiltration

| Technique | Name                                                         |
| --------- | ------------------------------------------------------------ |
| T1567.002 | Exfiltration Over Web Service: Exfiltration to Cloud Storage |
| T1041     | Exfiltration Over C2 Channel                                 |

## Impact

| Technique | Name                      |
| --------- | ------------------------- |
| T1486     | Data Encrypted for Impact |
| T1490     | Inhibit System Recovery   |
| T1657     | Financial Theft           |

---

# 9. Defensive Priorities

Based on the documented attack lifecycle, defensive priorities include:

### Reconnaissance

Monitor external exposure of critical applications and privileged-user information.

### Weaponization

Monitor threat intelligence for new FIN7 malware, loaders, domains and infrastructure.

### Delivery

Strengthen:

* Email filtering
* Attachment analysis
* URL reputation analysis
* Removable-media controls

### Exploitation

Prioritize rapid patching of internet-facing applications and monitor exploitation attempts against critical enterprise infrastructure.

### Persistence

Monitor for:

* New scheduled tasks
* Suspicious services
* Registry Run keys
* SSH services
* Suspicious persistence mechanisms

### Command & Control

Monitor:

* Anomalous DNS
* Unusual outbound connections
* Remote-management tools
* Non-standard ports
* Suspicious tunneling

### Actions on Objectives

Detect:

* Abnormal data staging
* Cloud uploads
* Privileged-account abuse
* Credential theft
* Ransomware behavior

---

# 10. Intelligence Gaps

## Current FIN7 Infrastructure

There is limited visibility into currently active:

* IP addresses
* Domains
* URLs
* C2 servers
* Hosting infrastructure

Many publicly documented indicators are historical and may no longer be operational.

## Current Targeting

More recent victim information is required to determine FIN7's current sector and geographic priorities.

## New TTPs & Vulnerabilities

Additional evidence is required regarding:

* Newly exploited CVEs
* Emerging TTPs
* Technologies currently targeted by FIN7

## Attribution

FIN7 has been associated with multiple criminal groups, ransomware operations, malware families and activity clusters.

Further evidence is required to distinguish confirmed FIN7 activity from suspected or low-confidence FIN7-associated activity.

---

# 11. Key CTI Takeaways

### 1. Threat actors evolve

FIN7 demonstrates how a financially motivated actor can expand beyond its historical focus and adopt broader enterprise intrusion and extortion operations.

### 2. Static IOC-based detection has limitations

Historical infrastructure can become inactive or change. Behavioral and TTP-based detection can therefore complement IOC-based detection.

### 3. ATT&CK mapping improves detection context

Mapping observed behavior to MITRE ATT&CK helps translate threat reporting into techniques that SOC and threat-hunting teams can investigate.

### 4. Intelligence gaps matter

A CTI assessment should identify not only what is known, but also what remains unknown and requires additional collection.

---

# 12. References

1. Blackpoint Cyber / Adversary Pursuit Group — FIN7 Threat Profile
2. Google Cloud / Mandiant — Evolution of FIN7
3. MITRE ATT&CK — FIN7 (G0046)
4. PRODAFT — FIN7-related infrastructure research

---

## Disclaimer

This document is intended for **defensive cybersecurity research and threat-intelligence purposes**.

The IOCs, infrastructure and threat information presented in this research are based on publicly documented reporting and should be independently validated before operational use.

**TLP:CLEAR**
