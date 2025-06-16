# 🛡️ Microsoft Sentinel 2025 – Home SOC Lab

This project simulates a **Home Security Operations Center (SOC)** using **Microsoft Azure** and **Microsoft Sentinel**. Built entirely from scratch, the lab captures real attack data by exposing a honeypot VM to the public internet, forwarding logs to Sentinel, enriching them with geolocation data, and visualizing global attacker activity.

> ✅ Successfully completed and documented by **Phanindhar Reddy Karnati** on **June 14, 2025**.

---

## 📁 Repository Structure

| Folder/File                  | Description                                                                 |
|-----------------------------|-----------------------------------------------------------------------------|
| `/docs/Microsoft_sentinel_2025.docx` | Full written report (Word format) documenting the entire lab            |
| `/docs/Microsoft_sentinel_2025.pdf`  | Same report in PDF format for easy viewing                             |
| `/docs/Lab_Checklist.docx`           | Step-by-step checklist used to build the lab                           |
| `/data/geoip-summarized.csv`         | GeoIP mapping file used as a watchlist in Sentinel                     |
| `/sentinel/map.json`                 | Sentinel Workbook (heatmap) template showing attacker IP visualization |
| `/assets/screenshots/`              | (Optional) Folder for lab process screenshots                          |

---

## 🧠 Key Learning Objectives

| Concept                         | Description                                                                 |
|----------------------------------|-----------------------------------------------------------------------------|
| SIEM (Microsoft Sentinel)        | Configure, monitor, and investigate incidents in a cloud-native SIEM        |
| Azure Infrastructure             | Deployed VM, NSG, VNet, LAW, and Sentinel from scratch                      |
| Log Forwarding & AMA             | Connected VMs to Log Analytics Workspace using Azure Monitor Agent (AMA)    |
| Kusto Query Language (KQL)       | Queried failed login logs and joined data with GeoIP watchlist              |
| Watchlist + Enrichment           | Merged IP logs with geolocation CSV for better insight                      |
| Visualization with Workbooks     | Created a live heatmap showing attacker geographies in real time            |

---

## 🏗️ Lab Architecture Overview

1. **Azure VM Honeypot** (Windows 10)
2. **Network Security Group** – all inbound traffic allowed
3. **Firewall disabled** – logs all attack attempts
4. **Event Viewer** – confirms failed login logs (Event ID 4625)
5. **Log Analytics Workspace** – central repository for logs
6. **Microsoft Sentinel** – SIEM setup for detection and queries
7. **GeoIP Watchlist** – uploaded CSV for IP-to-location mapping
8. **Sentinel Workbook** – interactive global map of attacker origins

---

## 🔍 Example KQL Query Used

```kusto
let geo = _GetWatchlist("geoip");
SecurityEvent
| where EventID == 4625
| lookup kind=leftouter geo on $left.IPAddress == $right.Network
| project TimeGenerated, Account, IPAddress, CityName, CountryName, Latitude, Longitude
```

---

## 🛠️ Tools & Platforms

| Tool                     | Purpose                                      |
|--------------------------|----------------------------------------------|
| Microsoft Azure          | Cloud infrastructure and virtual machines    |
| Microsoft Sentinel       | SIEM platform for log monitoring             |
| Azure Monitor Agent (AMA)| VM-to-LAW log forwarding                     |
| Event Viewer             | Local verification of log generation         |
| GitHub                   | Project repository and version control       |
| Kusto Query Language     | Log searching, filtering, and correlation    |

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).
