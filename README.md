# Splunk SIEM Lab: BOTSv1 Attack Log Analysis

**Project Overview**  
Simulated a Security Operations Center (SOC) environment using Splunk to analyze the **BOTSv1 dataset**, identifying malicious activity patterns and visualizing high-risk anomalies.

## 🔍 Key Features
- **Detected high-risk hosts** (e.g., `splunk-02` with 4,300+ errors).  
- **Correlated error spikes** (`timeout`, `critical`) with potential DoS/scanning activity.  
- **Built interactive dashboards** for real-time monitoring.  

## 🛠️ Tools & Technologies  
- **Splunk Enterprise** (Free Tier)  
- **SPL (Search Processing Language)**  
- **Regex** for field extraction  
- **Timechart visualizations**  

## 📊 Dashboard Panels  
1. **Top Error Hosts**  
   - Query: `index=botsv1 ("error" OR "fail*") | stats count by host | sort -count`  
   - Insight: Prioritized `splunk-02` for investigation due to abnormal error volume.  

2. **Error Trends Over Time**  
   - Query: `index=botsv1 earliest=0 ("error" OR "fail*") | timechart span=1h count by host`  
   - Insight: Spikes at specific intervals suggested scanning behavior.  

3. **Error Type Breakdown**  
   - Query: `index=botsv1 | rex field=_raw "(?<error_term>error|fail|critical|denied|timeout)" | stats count by error_term`  
   - Insight: `timeout` (81K events) and `critical` (20K events) dominated logs.  

## 🚨 Threat Analysis  
- **Potential DoS Attacks**: High `timeout` rates aligned with resource exhaustion patterns.  
- **Reconnaissance Activity**: `suricata-ids` host showed irregular spikes (2,387 events at 04:00).  
- **False Positives**: Distinguished misconfigurations (`refused`) from malicious events (`denied`).  

## 📂 Files in This Repo  
- `splunk_queries.txt`: SPL queries for detection.  
- `dashboard_screenshots/`: Visualizations of panels.  
- `BOTSv1_analysis_report.pdf`: Full findings and recommendations.  

## 🎯 Skills Demonstrated  
- **SIEM log analysis**  
- **SPL query optimization**  
- **Threat correlation** (error trends → attack patterns)  
- **Dashboard design** for SOC workflows  

## 💡 How to Replicate  
1. Download the [BOTSv1 dataset](https://www.splunk.com/en_us/blog/security/botsv1-download.html).  
2. Import into Splunk and run the provided SPL queries.  
3. Customize dashboards using the `timechart` and `stats` commands.  

## 🌟 Why This Matters  
This project mirrors real-world SOC tasks, showcasing:  
✅ **Proactive monitoring** of error anomalies.  
✅ **Data-driven decision-making** for incident response.  
✅ **Tool proficiency** with Splunk, a top SIEM in the industry.  
