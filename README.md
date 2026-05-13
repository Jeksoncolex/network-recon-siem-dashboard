# 🛡️ Enterprise SIEM Engineering: Automated Network Reconnaissance & Splunk Analytics

## 📋 1. Introduction
In modern enterprise cybersecurity operations, establishing rapid perimeter visibility and tracking operational configuration drift is critical. This project demonstrates how **Nmap** can be systematically engineered for advanced host discovery and network reconnaissance, and how **Splunk Enterprise** can be leveraged as a centralized SIEM for data ingestion, complex event parsing, security visualization, and automated alerting metrics. By combining scanning utilities with big-data analytics platforms, this lab builds an active monitoring framework capable of detecting exposed assets, monitoring network mutations over time, and throwing instant alerts against high-risk anomalies.

---

## 🎯 2. Objectives
- **Strategic Asset Mapping:** Conduct high-fidelity network sweeps to isolate live targets, open port maps, and application service banners.
- **Structured Log Generation:** Export raw reconnaissance data arrays into normalized, parser-ready XML formats to streamline downstream SIEM ingestion.
- **SIEM Ingestion Pipelines:** Onboard, categorize, and index unstructured configuration schemas into a central Splunk data index cluster.
- **Security Dashboard Architecture:** Build interactive Splunk visualization views to present actionable, real-time perimeter landscape telemetry.
- **SIEM Alert Engineering:** Design automated alert logic parameters inside Splunk to flag:
  - Detection of unmapped, unauthorized active host nodes.
  - Exposure of critical, high-risk operational destination ports.
  - Unexpected or unannounced service version changes on active infrastructure.

---

## 🛠️ 3. Tools & Infrastructure Matrix
- **Network Discovery Tool:** Nmap (Network Mapper) for signature scanning, service enumeration, and OS fingerprinting.
- **SIEM Core:** Splunk Enterprise (Local Instance) for log aggregation, pattern searching, dashboard creation, and rule alerting.
- **Validation Sandbox:** Isolated virtual subnet range configured to simulate live host scanning without impacting production service stability.
- **Deployment Environments:** Kali Linux (Reconnaissance Node), macOS (Centralized Splunk SIEM Monitoring Stack).
- **Hypervisor Core:** VMware Fusion.

---

## 🚀 4. Technical Methodology

### 4.1 Running Strategic Nmap Scans
Executed a targeted, multi-stage network scanning sequence to generate a complete footprint catalog of the target subnet:

#### 1. Passive Host Discovery (Ping Sweep)
Isolate live systems across the target block without initializing noisy port connections.
```bash
nmap -sn 192.168.1.95/24
```

#### 2. Localized Destination Port Discovery
Scan primary communication channels across targeted endpoints to discover open connection pathways.
```bash
nmap -p 1-1000 192.168.95/24
```

#### 3. Application Service Version Enumeration
Probe listening connections to capture system banners and determine application version configurations.
```bash
nmap -sV 192.168.1.95
```

#### 4. Remote Operating System Footprinting
Analyze TCP/IP stack response signatures to accurately profile the remote operating system vendor.
```bash
nmap -O 192.168.1.95
```

#### 5. Aggressive Attack Surface Inspection
Consolidate OS mapping, service version validation, script engine execution, and traceroute into an intense profiling string.
```bash
nmap -A 192.168.1.95
```

#### 6. Structured XML Telemetry Serialization
Export comprehensive service scans directly into clean XML file formatting to guarantee smooth integration with Splunk.
```bash
nmap -sV -oX nmap_results.xml 192.168.1.95/24
```

### 4.2 Data Pipeline & File Synchronization
- Provisioned an isolated host-to-guest shared mount point across VMware Fusion to bridge the architecture gap between Kali Linux and macOS.
- Transported the output file `nmap_results.xml` directly into the dedicated Splunk data staging folder.

### 4.3 Data Ingestion Pipeline Setup
1. Authenticated to the primary management dashboard at **Splunk Web** (`http://localhost:8000`).
2. Navigated to the ingestion engine interface: **Settings** → **Add Data** → **Upload File**.
3. Picked the target data artifact: `nmap_results.xml`.
4. Mapped specific parsing criteria to the intake stream: `xml` or custom `nmap_logs` formatting configurations.
5. Allocated data streams to a dedicated storage index: `nmap_index`.
6. Finalized the submission and verified incoming data loops via active query auditing.

### 4.4 Advanced Splunk Analytics Queries
Drafted explicit Splunk Search Processing Language (SPL) strings to process raw telemetry datasets into security visibility maps:

#### Query 1: Global Open Port Inventory Summary
Queries the index target to capture and output all instances of open ports across monitored network landscapes.
```splunk
index=nmap_index "open"
```

#### Query 2: Open Port Metrics Density Matrix
Transforms indexed logs into metrics, mapping the exact open connection density count per active host target.
```splunk
index=nmap_index "open" | stats count by host
```

---

## 🖼️ 5. Visual Portfolio Case Study Evidence

### 🛡️ Core Verification & Exploratory Triage
*Isolating terminal command input constraints and auditing active default host-based rulesets prior to ingestion deployment scripts.*
![Terminal Syntax Discrepancy](screenshots/1-Nmap-Syntax-Error.png)
![Target UFW Active Rules](screenshots/4-Initial-Firewall-Rules.png)

### 🥷 Active Scanning & Network Reconnaissance Simulation
*Simulating explicit target sweeps from the adversary node via deep TCP/UDP mapping loops to build logging payloads.*
![Nmap Host Reconnaissance](screenshots/2-Suricata-Threat-Alerts.png)

### 📊 Defensive System Configuration Verification
*Reviewing persistent background service daemons and spinning up standard infrastructure protection matrices.*
![Suricata Systemd Initialization](screenshots/3-Suricata-Service-Status.png)
![Target UFW Hardening](screenshots/5-Activating-Host-Firewall.png)

### 🛑 Real-Time Telemetry Audit & Perimeter Hardening Action
*Parsing active alert telemetry indices and committing immediate access control drop policies at the target firewall boundary.*
![Target UFW Rule Enforcement](screenshots/6-Enforcing-Deny-Policy.png)
![Target UFW Rule Enforcement 2](screenshots/7-Verifying-Blocked-IP.png)

---

## 📈 6. Results & Security Metrics
The end-to-end telemetry pipeline achieved all security monitoring parameters:
- **Exposed Surface Visibility:** Successfully isolated and registered active target inventories along with their explicit port layouts.
- **Threat Vector Containment:** Validated the detection of high-risk network ports as soon as they were exposed on monitored segments.
- **Version Tracking Accuracy:** Monitored system changes down to individual service version signatures to identify unpatched configurations.

---

## 🧠 7. Conclusion
 This lab demonstrates a functional architecture pattern for proactive internal network auditing. By linking scanning engines directly with structured log ingestion pipelines and big-data analytics platforms, defensive teams can spot infrastructure drift, pinpoint hidden vulnerabilities, and apply defensive countermeasures before a threat escalates into a full-scale compromise.

---

## 🔮 8. Operational Security Recommendations
- **Automated Scanning Schedules:** Deploy cron scripts to automatically execute scanning routines at standardized daily cycles.
- **Vulnerability Data Enrichment:** Ingest parallel vulnerability assessment telemetry from engines like OpenVAS into `nmap_index` for deeper risk context.
- **Incident Response Automation:** Configure Splunk alert actions to automatically forward high-severity detections straight to workflow managers (e.g., Jira Security/ServiceNow) to minimize mean time to remediation (MTTR).

---

## 👨‍💻 Author
**Sunday Ojeka**  
*Cybersecurity Specialist & Aspiring SOC Analyst*  
Focused on Security Log Orchestration, Infrastructure Reconnaissance, and SIEM Alert Architecture.
