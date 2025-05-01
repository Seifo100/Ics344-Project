# Phase 2: Visual Analysis with a SIEM Dashboard
In this phase we demonstrates the execution and monitoring of an SSH brute-force attack on a vulnerable system (Metasploitable3), using Splunk in kali as the SIEM platform for real-time log analysis and visualization.

We accessed the splunk server via http://kali:8000 and we installed Splunk Universal Forwarder on Metasploitable
## Log Visualization & Analysis
### Figure 1 – Raw Accepted Logins

![Screenshot 2025-05-02 012307](https://github.com/user-attachments/assets/7ac5f4f6-5d30-46a8-bd57-d45c0f6f67c5)
#### Query used: source="/var/log/auth.log" | where searchmatch("Accepted password")
Description: A detailed table view of the exact timestamps, users, and source IPs associated with successful logins.

All successful SSH logins were made by vagrant from 192.168.8.31, proving that the brute-force attack was eventually successful.This figure is a Log-level evidence that ties the attack IP to actual compromise.

### Figure 2 – Overall Auth Summary 
![Screenshot 2025-05-02 012526](https://github.com/user-attachments/assets/b882c3d3-5543-4b91-9ec3-6faf5ba99f3f)
#### Query Used: source="/var/log/auth.log" ("Failed password" OR "Accepted password") | eval Result=if(searchmatch("Failed password"), "Failed", "Accepted") | stats count by Result

Description: A bar chart comparing total failed logins against accepted ones.

Results: 138 failed vs 3 accepted logins.This is a simplified summary of authentication outcomes, great for executive overview or incident reporting.

### Figure 3 – Failed vs Successful Attempts per IP
![Screenshot 2025-05-02 012701](https://github.com/user-attachments/assets/eac4b18c-232d-45c4-acde-0956bf8ec5b3)
#### Query Used: source="/var/log/auth.log" ("Failed password" OR "Accepted password") | rex "for .* from (?<src_ip>\d+.\d+.\d+.\d+)" | stats count(eval(searchmatch("Failed password"))) as fails, count(eval(searchmatch("Accepted password"))) as succ by src_ip | eval ratio = fails/(succ+0.1) | where ratio > 10 | sort - ratio

Description: A multicolored bar chart showing the number of failed logins (purple), successful logins (pink), and calculated ratio (green) for each IP.

Results: IP 192.168.8.31 made 138 failed attempts and 3 successes. The calculated brute-force ratio is 45:1. This is a strong visual proof of high-volume brute force behavior concentrated from a single source.

### Figure 4 – Session Activity Analysis
![Screenshot 2025-05-02 012815](https://github.com/user-attachments/assets/2463a190-ab43-4b75-9b23-a62322a3210a)
#### Query Used:source="/var/log/auth.log" | eval event=case(searchmatch("session opened"), "open", searchmatch("session closed"), "close") | stats count by event

Description: This bar chart shows two categories: session opened and session closed, plotted on the X-axis. The Y-axis represents the number of events.

Results: 48 sessions were opened while only 36 were closed. This is a clear sign that some sessions remained active or were forcefully terminated.

