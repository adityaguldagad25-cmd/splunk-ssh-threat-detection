#Splunk SSH Threat Detection
1. Project Overview
This project uses Splunk Enterprise to analyze SSH authentication logs and identify failed and successful login activity.

The project uses simulated log data for cybersecurity learning and demonstrates basic SIEM log analysis.
2. Project Objectives
- Identify failed login attempts.
- Find usernames targeted by login attempts.
- Identify source IP addresses associated with failed logins.
- Review successful authentication events.
- Create a Splunk dashboard to display findings.
3. Tools and Technologies
- Splunk Enterprise
- Search Processing Language (SPL)
- SSH Authentication Logs
- GitHub
- Windows
4. Project Workflow
1. Create sample SSH authentication logs.
2. Upload the log file to Splunk.
3. Configure the source type.
4. Search and filter authentication events.
5. Extract usernames and source IP addresses.
6. Analyze failed and successful logins.
7. Create a dashboard.
8. Document the results on GitHub.
5. Sample Log Data
The dataset contains six simulated SSH authentication events.
Event Type	Count
Failed login attempts	4
Successful logins	1
Connection closed during authentication	1
Total events	6

6. SPL Queries and Analysis
6.1 Failed Login Attempts
Purpose: Searches for SSH events containing failed password attempts.
6.2 Failed Logins by Username
index=* sourcetype=linux_secure "Failed password"
| rex "Failed password for (?:invalid user )?(?<username>\S+)"
| stats count by username


Purpose: Extracts usernames and counts failed login attempts for each username.
6.3 Successful Logins
index=* sourcetype=linux_secure "Accepted password"
| rex "Accepted password for (?<username>\S+)"
| stats count by username


Purpose: Identifies usernames associated with successful password authentication.
6.4 Failed Login Attempts by Source IP
index=* sourcetype=linux_secure "Failed password"
| rex "from (?<src>\d{1,3}(?:\.\d{1,3}){3})"
| stats count by src


Purpose: Extracts source IP addresses and counts failed login attempts from each address.
7. Dashboard
The Splunk dashboard contains three panels:
- Failed Login Attempts by IP
- Successful Logins by Username
- Failed Logins by Username
These panels summarize authentication activity and make the results easier to review.
8. Sample Findings
- Four failed login attempts were recorded.
- The source IP 192.0.2.15 was associated with all four failed attempts.
- The usernames admin, root, test, and guest each had one failed attempt.
- One successful login was recorded for the username aditya.
- One additional event recorded a connection closed during authentication.
9. Security Observations
Repeated failed login attempts can indicate password guessing or a possible brute-force attempt. However, these sample events alone do not prove that a real attack occurred.

Security analysts should investigate the source, timing, frequency, and related events before drawing conclusions.
10. Limitations
- The dataset contains only six simulated events.
- The results do not represent real production traffic.
- The sample is too small to establish a real attack pattern.
- This project demonstrates basic log analysis, not a complete production SIEM deployment.
11. Future Improvements
- Analyze a larger SSH log dataset.
- Add time-based visualizations.
- Create alerts for repeated failed logins.
- Include more authentication event types.
- Investigate events using additional security logs.
12. Dashboard Screenshot
13. Disclaimer
This project uses simulated training data for educational purposes. The IP addresses and events are examples and do not establish malicious activity by any real system.
14. Author
Aditya Guldagad

Cybersecurity Learner | Interested in SOC Analysis, SIEM, and Threat Detection
