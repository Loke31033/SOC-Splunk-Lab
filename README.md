# 🔐 SOC Attack Detection & Incident Response Lab (Splunk + MITRE ATT&CK)

## 📌 Overview

This project demonstrates a complete **Security Operations Center (SOC) lab** where real-world cyber attacks are simulated, detected, investigated, and responded to using **Splunk SIEM**.

The lab follows the **MITRE ATT&CK framework**, covering the full attack lifecycle from **Initial Access to Defense Evasion**.

---

## 🎯 Objectives

- Simulate real-world cyber attacks using Kali Linux
- Collect and analyze logs from Windows 11 using Splunk
- Detect malicious activities using SPL queries
- Perform investigation and incident response
- Map attacks to MITRE ATT&CK framework

---

## 🧱 Lab Architecture

- **Attacker**: Kali Linux  
- **Victim**: Windows 11  
- **SIEM**: Splunk (Ubuntu Server)  
- **Log Source**: Windows Event Logs (Security)

📷 Architecture Diagram:

![Architecture](architecture.png)

---

## ⚙️ Tools & Technologies

- Splunk SIEM  
- Kali Linux (Hydra, RDP tools)  
- Windows 11  
- PowerShell  
- MITRE ATT&CK Framework  

---

## 🔥 Attack Scenarios Covered

### 🔹 Scenario 1 — Brute Force Attack (Initial Access)
- EventCode: 4625  
- Tool: Hydra  
- Detection: Failed login spike  

---

### 🔹 Scenario 2 — Account Compromise
- EventCode: 4624 + 4625  
- Detection: Failed + Success correlation  

---

### 🔹 Scenario 3 — PowerShell Execution
- EventCode: 4688  
- Detection: EncodedCommand  

---

### 🔹 Scenario 4 — Persistence
- Registry Run Keys  
- Scheduled Tasks  

---

### 🔹 Scenario 5 — Privilege Escalation
- EventCode: 4728, 4672  
- Detection: Admin group changes  

---

### 🔹 Scenario 6 — Credential Access
- LSASS targeting  
- Detection via process logs  

---

### 🔹 Scenario 7 — Lateral Movement
- EventCode: 4624 (Logon Type 10)  
- Detection: Remote login  

---

### 🔹 Scenario 8 — Data Exfiltration
- Tools: curl  
- Detection: Outbound command execution  

---

### 🔹 Scenario 9 — Defense Evasion
- EventCode: 1102  
- Detection: Log clearing  

---

## 🔍 Sample SPL Queries

### Brute Force Detection
```spl
index=windows EventCode=4625
| stats count by Source_Network_Address
| where count > 10

Account Compromise Detection

index=windows (EventCode=4624 OR EventCode=4625)
| stats count(eval(EventCode=4625)) AS failed,
        count(eval(EventCode=4624)) AS success
        by user, Source_Network_Address
| where failed > 5 AND success > 0

PowerShell Detection

index=windows EventCode=4688
| search Command_Line="*EncodedCommand*"


🚨 SOC Workflow Implemented
	1.	Detection — Identify suspicious activity
	2.	Investigation — Analyze logs and timeline
	3.	Response — Contain and remediate
	4.	Reporting — Document incident

🧠 MITRE ATT&CK Coverage

Tactic	Technique
Initial Access	Brute Force (T1110)
Execution	PowerShell (T1059)
Persistence	Registry Run Keys (T1547)
Privilege Escalation	Account Manipulation (T1098)
Credential Access	OS Credential Dumping (T1003)
Lateral Movement	Remote Services (T1021)
Exfiltration	Data Transfer (T1041)
Defense Evasion	Log Clearing (T1070)


⸻

📸 Screenshots

Each scenario includes:
	•	Attack simulation
	•	Splunk detection
	•	Investigation
	•	Response

📄 Project Structure

SOC-Splunk-Lab/
│
├── README.md
├── architecture.png
├── Scenario-1-BruteForce/
├── Scenario-2-Compromise/
├── Scenario-3-Execution/
├── Scenario-4-Persistence/
├── Scenario-5-PrivilegeEscalation/
├── Scenario-6-CredentialAccess/
├── Scenario-7-LateralMovement/
├── Scenario-8-Exfiltration/
├── Scenario-9-DefenseEvasion/

🚀 Key Skills Demonstrated
	•	SIEM Monitoring (Splunk)
	•	Log Analysis (Windows Event Logs)
	•	Incident Detection & Response
	•	Threat Detection using SPL
	•	MITRE ATT&CK Mapping
	•	Cyber Attack Simulation

🎯 Conclusion

This project demonstrates practical SOC analyst skills including detection, investigation, and response to real-world attack scenarios using Splunk.


👨‍💻 Author

Lokeshwar V
🔗 LinkedIn￼
💻 GitHub￼
