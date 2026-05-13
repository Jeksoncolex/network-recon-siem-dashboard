# 🛡️ Defensive Security Engineering: Automated Incident Response & Network Containment

## 📋 1. Objective & Scenario Overview
This project simulates a real-world cyber reconnaissance attack to demonstrate the structural execution of the industry-standard Incident Response (IR) lifecycle. Utilizing an offensive machine to simulate adversarial probing, this lab focuses on the engineering steps required to detect malicious behavior via an Intrusion Detection System (IDS), isolate systemic network telemetry, and execute perimeter containment using host-based firewalls to successfully mitigate live threats.

---

## 🏗️ 2. Environment Architecture & Tool Matrix
*   **Victim Endpoint Engine:** Ubuntu Server Node (`jekson@Jek`)
*   **Adversary Simulation Node:** Kali Linux Engine (`jeksontech@Jekson`)
*   **Network Fabric:** Isolated Virtual Subnet Environment (VMware Fusion)
*   **Defensive Telemetry Core:** Suricata IDS (Signature-based Deep Packet Inspection)
*   **Traffic Enforcement Layer:** Uncomplicated Firewall (UFW)
*   **Reconnaissance Engine:** Network Mapper (Nmap)

---

## 🚀 3. Technical Methodology (Incident Response Lifecycle Steps)

### 🛠️ Step 3.1: Preparation (Infrastructure Hardening)
The local host defenses were prepared by updating system packages, installing the active threat parsing engine, verifying the initial baseline states, and initiating tracking hooks on terminal command syntax configurations.

```bash
# Installing security dependencies and initializing alert stream tracking
sudo apt update && sudo apt install suricata -y
sudo tail -f /var/log/suricata/fast.log
```

#### 🖼️ Lab Evidence: Initial Initialization & Baseline Validation
![Terminal Syntax Discrepancy](screenshots/Nmap-Syntax-Error.png)
![Target UFW Active Rules](screenshots/Initial-Firewall-Rules.png)

---

### 🔍 Step 3.2: Identification (Detection & Telemetry Analysis)
The attacker node launched an intense, noise-heavy TCP SYN and UDP reconnaissance probe against the victim asset (`192.168.1.80`). The Suricata engine instantly trapped the malicious packet patterns, generating localized high-severity logs and revealing the adversary's source address: `192.168.1.72`.

```bash
# Offensive action launched from Kali Linux adversary node
nmap -sS -sU 192.168.1.80
```

#### 🖼️ Lab Evidence: Intrusion Alerts & Malicious Fingerprint Capture
![Nmap Host Reconnaissance](screenshots/Suricata-Threat-Alerts.png)

---

### 🛑 Step 3.3: Containment (Threat Isolation & Access Control)
To stop the adversary's lateral movements and infrastructure probing, the persistent background daemon status was checked, the host firewall subsystem was activated, and a strict rule was committed to block all inbound traffic from the malicious IP address (`192.168.1.72`).

```bash
# Committing host isolation rules inside the Linux kernel tables
sudo ufw enable
sudo ufw deny from 192.168.1.72
```

#### 🖼️ Lab Evidence: Defensive Engine Launch & Access List Enforcement
![Suricata Systemd Initialization](screenshots/Suricata-Service-Status.png)
![Target UFW Hardening](screenshots/Activating-Host-Firewall.png)

---

### 🧯 Step 3.4: Eradication & Verification Auditing
Active firewall state tables were audited to ensure the blocking policy was properly applied to the network stack. A follow-up scan from the attacker's system confirmed the host completely dropped all incoming traffic from that source, changing the port statuses from "open" to "filtered".

```bash
# Validating numbered firewall parameters
sudo ufw status numbered
```

#### 🖼️ Lab Evidence: Perimeter Security Auditing & Drop Traffic Verification
![Target UFW Rule Enforcement](screenshots/Enforcing-Deny-Policy.png)
![Target UFW Rule Enforcement 2](screenshots/Verifying-Blocked-IP.png)

---

### 🔄 Step 3.5: Recovery (Post-Incident Surveillance)
*   **System Integrity:** Target endpoint services remained fully accessible and functional for legitimate network clients.
*   **Persistent Monitoring:** Follow-up auditing loops were kept active to spot any multi-vector attack escalations or IP-spoofing changes:
    ```bash
    tail -f /var/log/suricata/fast.log
    ```

---

## 📈 4. Key Lessons Learned
*   **Passive Detection is Insufficient:** Relying solely on passive IDS detection is not enough; it must be backed by a firewall mechanism to actively stop ongoing security threats.
*   **Containment Controls Speed Matters:** Manual containment works well in labs, but automated blocking rules are essential to keep up with fast, automated scanning tools.
*   **Automation is Essential:** In real production environments, Suricata should run in **Intrusion Prevention System (IPS)** mode to automatically block threats through netfilter/iptables rules the moment an alert is triggered.

---

## 👨‍💻 Author
**Sunday Ojeka**
*Aspiring SOC Analyst | Cybersecurity Specialist*
Focused on Blue Team Operations and Security Automation.
