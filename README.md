# Splunk SOC Monitoring Lab

A hands-on Security Operations Centre analyst lab built in Splunk Enterprise — writing SPL queries, detecting threat patterns, building saved reports, configuring scheduled alerts, and assembling a live SOC dashboard from real log data.

---

## Project at a Glance

| | |
|---|---|
| **Tools Used** | Splunk Enterprise · SPL (Search Processing Language) · Splunk Dashboard Studio |
| **Platform** | Splunk Enterprise (local instance) |
| **Languages** | SPL |
| **Security Focus** | Threat detection · Log analysis · Alert engineering · SOC dashboard building |
| **Frameworks** | MITRE ATT&CK · SOC analyst workflows |

## The Problem This Project Solves

A Security Operations Centre lives and dies by its ability to detect anomalies in log data before those anomalies become incidents. Raw logs from web servers, firewalls, and applications generate millions of events per day. Without structured queries, saved searches, and dashboards, security analysts are looking for needles in haystacks — manually sifting through data and missing the patterns that matter.

Splunk is the industry-standard SIEM (Security Information and Event Management) platform used in enterprise SOCs worldwide. Knowing how to write SPL queries, create saved reports, configure threshold-based alerts, and build monitoring dashboards is a core skill for any SOC analyst or security engineer.

This lab simulates the core workflows of a level-1 and level-2 SOC analyst: investigating audit logs, detecting traffic anomalies, identifying high-error components, and building a dashboard that gives the security team continuous visibility into the environment.

## What Was Built

### SPL Queries Written
Ten queries across internal and audit indexes covering:
- Traffic volume analysis and timecharts
- Burst detection (traffic spikes above threshold)
- User activity auditing by host and user
- Component error rate analysis
- Source IP investigation

### Key Findings

| Finding | Detail |
|---|---|
| Traffic spike detected | ~300 kbps burst on April 18 — consistent with burst or DDoS-pattern traffic |
| Error-generating components | 7 components identified including HttpClientRequest and ExecProcessor |
| UI access events | 547 events across 145 unique user/path combinations |
| Audit activity | Search activity filtered and segmented by host for anomaly review |

### Saved Reports (4)
Version-controlled SPL queries saved for recurring analyst use — reproducible on demand without rewriting the search.

### Scheduled Alert (1)
Weekly alert configured to trigger when result count exceeds 1000. Demonstrates the threshold-based alerting pattern used in real SOC environments to page analysts for anomalous activity.

### SOC Dashboard (1)
A six-panel dashboard built in Dashboard Studio providing continuous visibility across:
- Traffic volume over time (area chart)
- Top source IPs (table)
- Error counts by component (bar chart)
- Audit activity by user (pie chart)
- Single-value KPI panels
- Search activity timechart

## Architecture

```
LOG SOURCES (internal index, audit index)
       |
       | Splunk ingestion
       v
SPLUNK ENTERPRISE
  ├── SPL Queries (10 searches)
  │     ├── Traffic volume analysis
  │     ├── Burst traffic detection (>threshold kbps)
  │     ├── Component error counts
  │     └── User audit activity by host
  │
  ├── Saved Reports (4)
  │     → reusable, scheduled or on-demand
  │
  ├── Alert: Weekly burst traffic check
  │     → triggers when results > 1000
  │     → simulates SOC page/notification
  │
  └── SOC Dashboard (6 panels)
        → continuous monitoring view
        → visible to all SOC analysts
```

## Key SPL Patterns Used

```splunk
# Traffic burst detection — find spikes above baseline
index=main | timechart span=1h sum(kbps) as traffic | where traffic > 200

# Component error analysis — identify noisy components
index=_internal log_level=ERROR | stats count by component | sort -count

# Audit activity by host — monitor who is searching what
index=_audit action=search | stats count by host, user | sort -count

# Burst traffic timechart — visualise traffic over time
index=main | timechart span=5m sum(kbps)
```

## Screenshots

| File | What It Shows |
|---|---|
| `audit-filtered-by-host.png` | Audit log filtered and segmented by Splunk host |
| `audit-search-activity.png` | User search activity across the audit index |
| `burst-traffic-timechart.png` | Timechart showing the April 18 traffic spike |
| `component-error-counts.png` | Error counts broken down by internal Splunk component |

## How to Reproduce

**Prerequisites:** Splunk Enterprise installed (free trial or licensed), sample data loaded into `main` and `_audit` indexes

```
1. Open Splunk Web (http://localhost:8000)
2. Run burst traffic detection query:
   index=main | timechart span=1h sum(kbps) as traffic
3. Run component error analysis:
   index=_internal log_level=ERROR | stats count by component | sort -count
4. Run user audit query:
   index=_audit action=search | stats count by host, user | sort -count
5. Save each query as a Report (Save As → Report)
6. Configure alert: Number of Results > 1000, Schedule: Weekly
7. Build dashboard in Dashboard Studio with 6 panels
```

## What This Demonstrates

- SPL query writing for security investigation and threat detection
- Splunk saved reports for recurring analyst workflows
- Threshold-based alert configuration (the pattern used in real SOC alerting)
- Dashboard Studio for building operational security monitoring views
- SOC analyst methodology: detect → investigate → report → monitor

---

*Oluwaseyi Michael Falode · Cybersecurity & Cloud Security Engineer · Toronto, ON*
