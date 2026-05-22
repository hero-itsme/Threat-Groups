
# Threat Actor Intelligence Repository: APT-41 (DOUBLE DRAGON)

[![Threat Tier: Nation-State](https://img.shields.io/badge/Threat%20Tier-Tier%201%20--%20Nation--State-red.svg)](#actor-profile)
[![Attribution Confidence: High](https://img.shields.io/badge/Attribution%20Confidence-High%20(84%25)-brightgreen.svg)](#analyst-assessment)
[![Last Updated](https://img.shields.io/badge/Last%20Updated-2026--05--18-blue.svg)](#changelog)

## 📖 Overview

This repository contains structured cyber threat intelligence (CTI), Indicators of Compromise (IOCs), and defensive playbooks tracking the Chinese state-sponsored threat actor **APT-41** (also known as *DOUBLE DRAGON, BARIUM, WINNTI GROUP, and WICKED PANDA*). 

APT-41 is highly unique due to its **dual-mission mandate**, seamlessly running state-directed espionage campaigns and financially motivated cybercrime operations (such as virtual currency fraud in the gaming sector) out of the same infrastructure.

This documentation serves as an operational guide for threat hunters, detection engineers, and security operations center (SOC) analysts to ingest, hunt for, and mitigate risks associated with APT-41.

---

## 📁 Repository Structure

```text
├── README.md                  # This documentation file
├── threat_report_apt41.md     # Full comprehensive Threat Actor Report
├── iocs/
│   └── iocs.txt               # Consolidated master list of defanged IOCs (IPs, Domains, Hashes)
