# Office-SOC-Infrastructure
Centralized SIEM &amp; EDR deployment for office security monitoring

# Enterprise SIEM & Endpoint Security Monitoring Infrastructure

## 🚀 Overview
Designed and deployed a centralized, production-grade security monitoring and threat detection infrastructure for an office environment. This project bridges the gap between traditional log management and modern endpoint monitoring, ensuring real-time visibility, log ingestion, and threat hunting capabilities across Windows office endpoints.

---

## 🛠️ Architecture & Technology Stack
* **Central Monitoring Host:** Kali Linux (acting as the central SIEM & management server)
* **Log Ingestion & SIEM:** Splunk Enterprise, utilizing Splunk Universal Forwarders on target Windows endpoints
* **EDR & Threat Intelligence:** Wazuh XDR/EDR (deployed via Docker containers) for advanced telemetry and File Integrity Monitoring (FIM)
* **Telemetry Sources:** Windows Security Event Logs, Sysmon (System Monitor)

---

## 🔍 Key Implementations & Detection Engineering

### 1. Active Threat Detection & SPL Queries
Built and scheduled custom real-time SPL (Search Processing Language) queries running on cron-based intervals (5-minute frequency) to catch critical attack vectors instantly:
* **Brute-Force Detection:** Monitoring Windows Event ID `4625` (Failed Logon) with source IP correlation to flag repetitive login failures.
* **Account Lifecycle Tracking:** Auditing unauthorized user account creation and deletion events.
* **Malicious Process Execution:** Monitoring Sysmon Event ID `1` for suspicious Command Line activity, obfuscated or encoded PowerShell commands (`-enc`, `*encodedcommand*`), and raw CMD script execution.
* **Antivirus Integration:** Integrating Windows Defender logs (`EventCode 1116`) into central SIEM alerts.

### 2. Alert Tuning & False Positive Reduction
* Conducted baseline analysis to filter out legitimate office background processes and utility binaries (such as application webviews and background browser runtimes like WebView2) to minimize alert fatigue and maintain high-fidelity incident notification.

---

## 📈 Future Enhancements
* Integrating Wazuh active response rules for automated endpoint isolation upon critical threat triggers.
* Expanding forensic data collection using automated log shippers.

