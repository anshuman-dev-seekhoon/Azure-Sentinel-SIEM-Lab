# Real-Time Cyber Attack Detection & Analysis using Azure Sentinel + KQL 🚀🔍🌍

![Dashboard Screenshot](screenshots)

## 🔧 Project Overview
This project showcases a **real-time cyber attack detection and analysis lab** using Microsoft Sentinel (formerly Azure Sentinel). It simulates and monitors live cyber threats by leveraging a honeypot VM, custom log analytics, and KQL-based threat analysis. This SIEM lab helped in understanding threat patterns and building skills in security monitoring, threat hunting, and log data enrichment.

> ⛔ **Note:** This project was built using an Azure free trial subscription which has since expired. Therefore, the live environment and KQL queries are no longer accessible. However, this repository includes **detailed documentation and screenshots** of the original setup, workflows, and analysis.

## 👁️ What It Detects
- ✅ Brute-force attacks (RDP, SSH)
- ✅ Port scanning attempts
- ✅ Unauthorized access attempts
- ✅ Suspicious login patterns
- ✅ Geolocation-based threat tracking

---

## 📊 Project Breakdown

### 1. Setting Up the SIEM Lab & Log Collection
- Deployed a **Windows VM honeypot** in Azure to attract cyber attacks.
- Connected the VM to **Log Analytics Workspace**.
- Enabled data collection for:
  - Failed logins (Event ID 4625)
  - Remote login attempts
  - Network activity logs
  - Security event logs

### 2. Enriching Log Data Using ipgeolocation.io API
- Integrated [ipgeolocation.io](https://ipgeolocation.io) API with KQL queries.
- Used attacker IPs from logs to fetch:
  - Country, State
  - Latitude, Longitude
- Enabled visualization of attack origin **on a world map dashboard**.

### 3. Custom KQL Queries for Threat Analysis
> Since live queries are not accessible anymore, below are **examples** of the types of queries used:

#### Example 1: Detecting RDP Brute-force Attempts
```kql
SecurityEvent
| where EventID == 4625 and LogonType == 10
| summarize Attempts=count() by Account, IPAddress, bin(TimeGenerated, 1h)
| where Attempts > 5
```

#### Example 2: Enriching with Geolocation Data (via API call)
```kql
ExternalData
| join kind=inner (SecurityEvent | where EventID == 4625) on IPAddress
| project TimeGenerated, Account, IPAddress, Country, Latitude, Longitude
```

#### Example 3: Port Scanning Attempt Detection
```kql
Heartbeat
| where RemoteIPCountry != ""
| summarize Scans=count() by RemoteIP, bin(TimeGenerated, 1h)
| where Scans > 20
```

### 4. Sentinel Workbook Visualizations
- Created custom **interactive dashboards** with:
  - World map of attacker IPs
  - Time-based trend graphs
  - Top attacking IPs and usernames
- Set up **alert rules** for high-frequency events and brute-force detections

---

## 🔥 Key Takeaways
- Hands-on experience with **SIEM and SOC operations**
- Learned and applied **Kusto Query Language (KQL)**
- Enhanced detection using **external API integration**
- Created professional dashboards and alerts
- Understood **real-world attack patterns and security events**

---

## 📅 Timeline & Tools
- **Platform:** Microsoft Azure (Sentinel, Log Analytics, VM)
- **Language:** KQL
- **API:** ipgeolocation.io
- **Duration:** 1 Week (Azure trial period)

## 📈 Screenshots
All screenshots are stored in the `/screenshots` folder. Key visuals include:
- `workbook_brute_force_attacks.jpg`
- `workbook_geolocation_tracking.jpg`
- `dashboard_suspicious_logins.jpg`
- `workbook_port_scans.jpg`

---

## 🚀 Inspiration
A special thanks to cybersecurity content from **Josh Madakor** and other online tutorials that guided the efficient setup of this project.

---

## 👋 Final Note
If you're a recruiter, cybersecurity enthusiast, or SIEM learner, feel free to fork or star the repo! I’m happy to connect and discuss this project.

---

> **This project is now archived for documentation and portfolio purposes.**

