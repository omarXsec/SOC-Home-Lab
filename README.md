# SOC Home Lab — Attack Detection with Splunk & MITRE ATT&CK

A home lab simulating a real SOC (Security Operations Center) environment built from scratch using VirtualBox. The lab includes a Windows Active Directory network, a Splunk SIEM, and simulated cyberattacks mapped to the MITRE ATT&CK framework with working detection alerts and a monitoring dashboard.

---

## Lab Architecture

| Machine | OS | Role | IP |
|---|---|---|---|
| DC01 | Windows Server 2022 | Domain Controller (lab.local) | 192.168.10.10 |
| PC01 | Windows 10 Pro | Domain Client (attack target) | 192.168.10.20 |
| Splunk | Ubuntu 22.04 | SIEM / Log Collector | 192.168.10.30 |

---

## Tools Used

- VirtualBox — hypervisor for running all VMs
- Active Directory — domain management and user authentication
- Splunk Enterprise — SIEM for log collection, detection, and dashboards
- Splunk Universal Forwarder — log forwarding agent installed on PC01
- MITRE ATT&CK Framework — attack simulation reference

---

## Project Phases

### Phase 1 — Network Setup

Built a three-VM internal network in VirtualBox. Installed and configured Active Directory Domain Services on DC01, created the domain lab.local, and joined PC01 to the domain.

### Phase 2 — Splunk SIEM Setup

Installed Splunk Enterprise on the Ubuntu VM. Installed the Splunk Universal Forwarder on PC01 to forward Windows Event Logs to Splunk for centralized monitoring.

### Phase 3 — Attack Simulation

Simulated three MITRE ATT&CK techniques on PC01 to generate real attack telemetry:

| Technique | ID | Event ID | Description |
|---|---|---|---|
| Brute Force | T1110 | 4625 | 50+ failed login attempts against local and domain accounts |
| Create Account | T1136 | 4720 | Created a backdoor user account named "hacker" |
| Privilege Escalation | T1078 | 4732 | Added "hacker" account to the Administrators group |

### Phase 4 — Detection & Monitoring

Built three Splunk saved search alerts (scheduled every 5 minutes) and a Classic Dashboard to monitor all three attack techniques in real time.

#### Detection Alerts

| Alert | Technique | Trigger Condition | Severity |
|---|---|---|---|
| T1110 - Brute Force Login Attempt | T1110 | 5+ failed logins in 5 minutes | High |
| T1136 - New User Account Created | T1136 | Any new account creation detected | High |
| T1078 - Privilege Escalation Detected | T1078 | Any account added to privileged group | Critical |

#### Dashboard

Built a Classic Dashboard titled "SOC Attack Detection Dashboard" with three panels:

- T1110 — Line chart showing brute force login attempts over time
- T1136 — Table showing new user accounts created
- T1078 — Table showing privilege escalation events

---

## Key Takeaways

- Gained hands-on experience building and managing an Active Directory environment
- Understood how Windows Event Logs are generated and forwarded to a SIEM
- Simulated real attacker techniques mapped to the MITRE ATT&CK framework
- Built working detection rules and a monitoring dashboard in Splunk
