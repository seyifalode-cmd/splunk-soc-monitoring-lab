SOC Analyst lab using Splunk — SPL queries, threat detection, alerts, and dashboard
# Splunk SOC Monitoring Lab

## What This Is
A hands-on SOC analyst lab using Splunk Enterprise. I investigated 
internal logs, detected burst traffic patterns, audited user activity, 
built 4 saved reports, configured a weekly alert, and built a full 
SOC monitoring dashboard.

## Tools Used
- Splunk Enterprise
- SPL (Search Processing Language)
- Splunk Dashboard Studio

## What I Built
- 10 SPL queries across internal and audit indexes
- 4 saved reports
- 1 weekly scheduled alert (triggers at >1000 results)
- 1 SOC dashboard with 6 panels (table, pie, bar, single value, area chart)

## Key Findings
- Detected a traffic spike to ~300 kbps on April 18 — consistent with burst/DDoS behavior
- Identified 7 error-generating components including HttpClientRequest and ExecProcessor
- Monitored 547 UI access events across 145 unique user/path combinations

## Dashboard Preview
![Dashboard](screenshots/14-dashboard-full-view.png)
