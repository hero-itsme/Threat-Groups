# 🛡️ Threat Actor Profiling Repository

A curated collection of detailed threat actor intelligence profiles covering Advanced Persistent Threats (APTs), cybercriminal groups, nation-state actors, ransomware operators, and other malicious cyber organizations.

This repository aims to provide cybersecurity professionals, threat hunters, SOC analysts, incident responders, researchers, and students with structured intelligence on threat actors, their tactics, techniques, procedures (TTPs), malware ecosystems, infrastructure, targeting patterns, and operational history.

---

## 🎯 Objectives

- Maintain structured threat actor intelligence profiles.
- Map adversary behavior to the MITRE ATT&CK framework.
- Document malware families, tools, and infrastructure used by threat actors.
- Support threat hunting, detection engineering, and incident response activities.
- Provide actionable defensive recommendations.
- Create a centralized reference for cyber threat intelligence (CTI) research.

---

## 📂 Repository Structure

```text
Threat-Groups/
│
├── APT-1.md
├── APT-28.md
├── APT-29.md
├── APT-37.md
├── APT-38.md
├── APT-41.md
├── Lazarus-Group.md
├── Mustang-Panda.md
├── FIN7.md
├── LockBit.md
├── BlackCat.md
└── ...
```

Each profile follows a standardized reporting format to ensure consistency across all threat actor assessments.

---

## 📋 Threat Actor Profile Template

Each threat actor report may include:

### Executive Summary
High-level overview of the threat actor and its significance.

### Actor Profile
- Aliases
- Origin/Country Attribution
- Suspected Sponsorship
- Active Since
- Motivation
- Confidence Assessment

### Key Findings
Summary of major observations and intelligence assessments.

### Targeted Sectors
- Government
- Defense
- Telecommunications
- Healthcare
- Financial Services
- Manufacturing
- Energy
- Technology
- Aviation
- Critical Infrastructure

### Geographic Targeting
Regions and countries commonly targeted.

### Attack Lifecycle Analysis
- Initial Access
- Execution
- Persistence
- Privilege Escalation
- Defense Evasion
- Credential Access
- Discovery
- Lateral Movement
- Collection
- Command & Control
- Exfiltration
- Impact

### MITRE ATT&CK Mapping
Mapped ATT&CK techniques and procedures used by the actor.

### Malware & Tooling
Examples:
- PlugX
- ShadowPad
- Cobalt Strike
- Mimikatz
- Winnti
- Poison Ivy
- Gh0st RAT

### Indicators of Compromise (IOCs)
- Domains
- IP Addresses
- File Hashes
- URLs
- Registry Keys
- Network Indicators

### Analyst Assessment
Threat evaluation, operational capability, and future outlook.

### Defensive Recommendations
Actionable security controls and detection guidance.

### References & Sources
Public reports, vendor research, advisories, and intelligence publications.

---

## 🗺️ Intelligence Frameworks Used

- MITRE ATT&CK
- Cyber Kill Chain
- Diamond Model of Intrusion Analysis
- Pyramid of Pain
- Intelligence Cycle Methodology

---

## 👥 Intended Audience

- Threat Intelligence Analysts
- SOC Analysts
- Incident Responders
- Threat Hunters
- Malware Analysts
- Digital Forensics Investigators
- Security Researchers
- Students and Educators

---

## ⚠️ Disclaimer

This repository is intended solely for educational, research, defensive security, and threat intelligence purposes. Information contained within these profiles is derived from publicly available intelligence sources and should not be used for unauthorized or malicious activities.

---

## 🤝 Contributions

Contributions are welcome.

Before submitting a profile:

1. Follow the established report format.
2. Include reputable intelligence sources.
3. Reference MITRE ATT&CK techniques where applicable.
4. Maintain objective and evidence-based analysis.
5. Verify indicators and attribution claims whenever possible.

---

## 📚 Recommended Sources

- MITRE ATT&CK
- CISA Advisories
- Mandiant Reports
- Microsoft Threat Intelligence
- CrowdStrike Intelligence
- Palo Alto Unit 42
- Recorded Future
- Cisco Talos
- Secureworks CTU
- SentinelLabs
- Proofpoint Research
- Trend Micro Research
- Kaspersky Securelist

---

## ⭐ Project Goal

To build a comprehensive, open-source repository of threat actor intelligence that helps defenders understand adversary behavior, improve detection capabilities, and strengthen organizational cyber resilience.

---

**Maintained by the Cyber Threat Intelligence Community**
