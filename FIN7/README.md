# FIN7 Threat Intelligence Research

![TLP](https://img.shields.io/badge/TLP-CLEAR-green)
![Threat Intelligence](https://img.shields.io/badge/Focus-Threat%20Intelligence-blue)
![MITRE ATT\&CK](https://img.shields.io/badge/MITRE%20ATT%26CK-Mapped-red)

## Overview

This repository contains a Cyber Threat Intelligence (CTI) research project focused on **FIN7 (G0046)**, a financially motivated cybercriminal group tracked by MITRE ATT&CK.

The research examines FIN7's evolution from payment-card theft toward broader **enterprise intrusion, data theft, initial-access operations, ransomware and extortion activity**.

The analysis combines threat-actor profiling, Cyber Kill Chain analysis, MITRE ATT&CK mapping, IOC analysis, malware/tooling research, vulnerability intelligence, defensive priorities, and identified intelligence gaps.

## Research Objectives

* Profile FIN7 and its known aliases
* Analyze FIN7's targeting and victimology
* Map documented activity across the Cyber Kill Chain
* Map FIN7 behaviors to MITRE ATT&CK
* Identify relevant IOCs and malware/tooling
* Analyze vulnerabilities associated with documented activity
* Derive defensive priorities for SOC and threat-hunting teams
* Identify intelligence gaps requiring further collection

## Key Findings

FIN7 has historically been associated with payment-card theft, particularly against retail, restaurant and hospitality organizations.

The research documents a broader operational scope involving:

* Enterprise intrusion
* Initial-access operations
* Credential theft
* Data collection and exfiltration
* Custom malware and loaders
* Ransomware-related activity
* Financial extortion

FIN7's documented tooling includes **CARBANAK, BIRDWATCH, POWERPLANT, LOADOUT, GRIFFON, POWERTRASH and DICELOADER**.

## MITRE ATT&CK Coverage

The research maps FIN7 activity across multiple ATT&CK tactics, including:

| Tactic               | Example Techniques                                           |
| -------------------- | ------------------------------------------------------------ |
| Reconnaissance       | T1591, T1591.004                                             |
| Resource Development | T1583.001, T1584.001, T1585.002                              |
| Initial Access       | T1566.001, T1566.002, T1190, T1189, T1199, T1195.002         |
| Execution            | T1059.001, T1059.003, T1059.005, T1059.007, T1204.002, T1047 |
| Persistence          | T1053.005, T1547.001, T1543.003                              |
| Privilege Escalation | T1068, T1548                                                 |
| Defense Evasion      | T1027, T1036, T1070.004, T1562.001                           |
| Credential Access    | T1003, T1558.003, T1078                                      |
| Discovery            | T1057, T1087.002, T1069.002, T1049, T1016, T1033             |
| Lateral Movement     | T1021.001, T1021.004, T1021.005, T1078                       |
| Command & Control    | T1071.001, T1071.004, T1105, T1090, T1572, T1102             |
| Collection           | T1005, T1113, T1123                                          |
| Exfiltration         | T1567.002, T1041                                             |
| Impact               | T1486, T1490, T1657                                          |

## Vulnerability Intelligence

The report identifies two vulnerabilities associated with documented FIN7 activity:

| CVE                       | CVSS | Patch Available |
| ------------------------- | ---: | --------------- |
| CVE-2021-31207            |  9.8 | Yes             |
| CVE-2020-1472 (ZeroLogon) | 10.0 | Yes             |

## IOC & Malware Analysis

The research includes:

* Endpoint artifacts
* PowerShell artifacts
* Suspicious commands
* Scheduled-task artifacts
* Network domains
* IP addresses
* TOR infrastructure
* Malware and tooling

Examples of documented tooling include:

* CARBANAK
* BOOSTWRITE
* Cobalt Strike
* AdFind
* PowerSploit / POWERTRASH
* DICELOADER
* STONEBOAT
* Atera

> **Note:** Historical IOCs should be independently validated before being used for blocking or detection because infrastructure may become inactive or be reassigned.

## Defensive Priorities

The analysis identifies several defensive focus areas:

* Monitor exposure of critical internet-facing applications
* Monitor privileged-user information
* Track emerging FIN7 malware, loaders and infrastructure
* Strengthen phishing and URL analysis
* Rapidly patch internet-facing applications
* Detect suspicious scheduled tasks and services
* Monitor Registry Run keys and SSH activity
* Detect anomalous DNS and outbound connections
* Monitor remote-management tools and non-standard ports
* Detect abnormal data staging and cloud uploads
* Monitor privileged-account activity and credential theft
* Detect ransomware-related behaviors

## Intelligence Gaps

The research identifies four major intelligence gaps:

1. **Current infrastructure** — limited visibility into currently active FIN7 IPs, domains, URLs and C2 infrastructure.
2. **Current targeting** — additional recent victim information is required to determine current sector and geographic priorities.
3. **New TTPs and vulnerabilities** — additional evidence is required regarding newly exploited vulnerabilities and evolving techniques.
4. **Attribution** — further evidence is required to distinguish confirmed FIN7 activity from suspected FIN7-associated or affiliate activity.

## Sources

The analysis is based primarily on publicly available threat-intelligence research from:

* MITRE ATT&CK
* Google Cloud / Mandiant
* Blackpoint Cyber / Adversary Pursuit Group
* PRODAFT

See `FIN7.md` for the detailed analysis and references.

## Disclaimer

This repository is intended for **defensive cybersecurity research and threat-intelligence analysis**.

The information represents publicly documented threat activity and should be independently validated before being used for operational detection, blocking or attribution.
