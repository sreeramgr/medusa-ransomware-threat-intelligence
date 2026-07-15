# Medusa Ransomware Threat Intelligence Report

## Project Overview

This report analyzes Medusa ransomware from a cyber threat intelligence perspective using publicly available reporting, including the CISA/FBI/MS-ISAC StopRansomware advisory and supporting notes prepared during review.

The goal of this report is to understand Medusa’s attack lifecycle, initial access methods, tools, tactics, techniques, procedures, exfiltration behavior, encryption activity, MITRE ATT&CK mapping, and recommended defensive actions.

This report is created for educational and portfolio purposes as part of threat intelligence learning and preparation for cybersecurity work.

---

## 1. Executive Summary

Medusa is a ransomware operation that uses a combination of initial access methods, living-off-the-land techniques, remote access tools, data exfiltration, and file encryption to compromise victim environments.

Based on the reviewed advisory and notes, Medusa actors may rely on Initial Access Brokers, phishing campaigns, exploitation of unpatched vulnerabilities, and abuse of legitimate administrative tools. After gaining access, the actors perform discovery, move laterally, exfiltrate data, stop critical services, delete shadow copies, and encrypt files using the `.medusa` extension.

The activity shows a modern ransomware pattern where attackers do not only encrypt files. They also steal data and use extortion pressure against victims. Because of this, organizations need strong identity security, patch management, network monitoring, segmentation, backup protection, and incident response planning.

---

## 2. Threat Overview

| Category                  | Details                                                                                                                                  |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Threat Name               | Medusa                                                                                                                                   |
| Threat Type               | Ransomware                                                                                                                               |
| Primary Motivation        | Financial gain                                                                                                                           |
| Attack Model              | Data theft, encryption, and extortion                                                                                                    |
| Initial Access Methods    | Initial Access Brokers, phishing, exploitation of unpatched vulnerabilities                                                              |
| Common Tools Observed     | SoftPerfect Network Scanner, PowerShell, Windows Command Prompt, WMI, Certutil, Ligolo, Cloudflared, AnyDesk, Atera, ConnectWise, Rclone |
| Encrypted File Extension  | `.medusa`                                                                                                                                |
| Notable Malware Component | `gaze.exe`                                                                                                                               |
| Main Impact               | Data encryption, service disruption, data theft, recovery pressure, possible public exposure of stolen data                              |

---

## 3. Initial Access

Medusa actors may use multiple methods to gain access to victim environments. One important method is the use of Initial Access Brokers, also known as IABs. These brokers obtain or sell access to victim systems, allowing ransomware actors to enter the environment without directly conducting the first stage of compromise themselves.

Common initial access methods include:

* Phishing campaigns
* Stolen or compromised credentials
* Exploitation of unpatched software vulnerabilities
* Abuse of exposed or vulnerable remote access services

The reviewed notes mention vulnerabilities such as ScreenConnect vulnerabilities and Fortinet EMS SQL injection as examples of software weaknesses that may be abused if systems are not patched.

From a defensive perspective, this shows that ransomware prevention must begin before encryption. Organizations should focus on reducing initial access opportunities through MFA, patching, phishing defense, account monitoring, and secure remote access.

---

## 4. Attack Lifecycle

A simplified Medusa ransomware attack lifecycle can be understood as follows:

### 4.1 Initial Access

The attackers first gain entry into the victim environment. This may happen through phishing, Initial Access Brokers, stolen credentials, or exploitation of vulnerable systems.

### 4.2 Discovery

After gaining access, the actors perform discovery to understand the victim’s network. This can include scanning ports, identifying services, checking system information, and enumerating files or network shares.

The reviewed notes mention the use of SoftPerfect Network Scanner and commonly scanned ports such as:

* 21 - FTP
* 22 - SSH
* 23 - Telnet
* 80 - HTTP
* 115
* 443 - HTTPS
* 1433 - Microsoft SQL Server
* 3050
* 3128
* 3306 - MySQL
* 3389 - RDP

This discovery activity helps attackers understand the environment and identify systems that may be useful for lateral movement, data theft, or ransomware deployment.

### 4.3 Living-off-the-Land Activity

Medusa actors may use legitimate tools already present in the environment. This is known as living-off-the-land, or LOTL. These tools can make detection harder because the activity may look similar to normal administrative behavior.

Examples from the reviewed notes include:

* PowerShell
* Windows Command Prompt
* Windows Management Instrumentation, also known as WMI
* Certutil.exe

These tools can be used for system discovery, file transfers, command execution, or other activity that supports the attack.

### 4.4 Defense Evasion

The actors may try to avoid detection by using legitimate utilities, clearing command history, using obfuscated or encrypted files, and disabling or modifying security tools.

The reviewed notes mention Certutil.exe as a tool that may be used during file transfer activity. The notes also identify defense evasion behaviors such as:

* Clearing command history
* Using obfuscated or encrypted files
* Disabling or modifying security tools
* Using legitimate tools to blend into normal activity

This makes monitoring important. Security teams should not only look for known malware, but also unusual use of normal tools.

### 4.5 Command and Control

Medusa activity may involve tools that support tunneling, remote communication, and attacker-controlled access.

Tools noted include:

* Ligolo, a reverse tunneling tool
* Cloudflared, which can expose services or servers through tunnels
* Remote access software such as AnyDesk, Atera, ConnectWise, eHorus, N-able, SimpleHelp, and Splashtop

These tools can help attackers maintain access, move through the environment, or communicate with attacker-controlled infrastructure.

### 4.6 Lateral Movement

After gaining access, attackers may move from one system to another. The reviewed notes mention several remote access and deployment tools that may be abused for lateral movement, including:

* RDP tools
* AnyDesk
* Atera
* ConnectWise
* eHorus
* N-able
* PDQ Deploy
* PDQ Inventory
* SimpleHelp
* Splashtop

The use of these tools is important because many of them are legitimate administration tools. If they are used without approval or from unusual accounts, they may indicate attacker activity.

### 4.7 Exfiltration

Before encryption, Medusa actors may exfiltrate data from the victim environment. The reviewed notes mention Rclone as a tool used to facilitate exfiltration of data to attacker-controlled servers or cloud storage.

This stage is important because ransomware incidents are not only about system recovery. If sensitive data is stolen, the victim may also face legal, regulatory, financial, and reputational impact.

### 4.8 Encryption and Impact

After exfiltration, Medusa actors may deploy ransomware to encrypt files. The reviewed notes mention that encrypted files may use the `.medusa` extension.

The notes also mention `gaze.exe`, which may terminate services related to backups, security, databases, communication, file sharing, and websites. It may also delete shadow copies and encrypt files using AES-256.

This behavior directly affects recovery because stopping services and deleting shadow copies can make restoration harder.

---

## 5. Tools and Observed Usage

| Tool                        | Possible Use in Attack                                      |
| --------------------------- | ----------------------------------------------------------- |
| SoftPerfect Network Scanner | Network discovery and port scanning                         |
| PowerShell                  | Command execution, file enumeration, discovery              |
| Windows Command Prompt      | Command execution and file or network enumeration           |
| WMI                         | Querying system information and possible remote execution   |
| Certutil.exe                | File transfer activity and living-off-the-land usage        |
| Ligolo                      | Reverse tunneling                                           |
| Cloudflared                 | Tunneling or exposing services                              |
| AnyDesk                     | Remote access                                               |
| Atera                       | Remote access or administration                             |
| ConnectWise                 | Remote access or administration                             |
| eHorus                      | Remote access                                               |
| N-able                      | Remote monitoring or administration                         |
| PDQ Deploy                  | Software deployment and possible lateral movement           |
| PDQ Inventory               | Asset and system inventory                                  |
| SimpleHelp                  | Remote access                                               |
| Splashtop                   | Remote access                                               |
| Rclone                      | Data exfiltration to cloud storage or remote infrastructure |
| gaze.exe                    | Service termination, shadow copy deletion, file encryption  |

---

## 6. MITRE ATT&CK Mapping

| Tactic              | Technique / Behavior                        | Explanation                                                                                                 |
| ------------------- | ------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Initial Access      | Phishing                                    | Phishing may be used to trick users into opening malicious content or giving away credentials.              |
| Initial Access      | Exploit Public-Facing Application           | Unpatched software vulnerabilities may be exploited to gain access.                                         |
| Initial Access      | Initial Access Brokers                      | Access may be obtained through brokers who provide entry into victim environments.                          |
| Execution           | PowerShell                                  | PowerShell may be used for command execution and system activity.                                           |
| Execution           | Windows Command Shell                       | Windows command shell may be used for execution and enumeration.                                            |
| Execution           | Windows Management Instrumentation          | WMI may be used to query systems or support remote activity.                                                |
| Persistence         | Create Account                              | Attackers may create accounts to maintain access.                                                           |
| Defense Evasion     | Clear Command History                       | Clearing history may remove traces of attacker activity.                                                    |
| Defense Evasion     | Obfuscated or Encrypted Files               | Obfuscation can make analysis and detection harder.                                                         |
| Defense Evasion     | Disable or Modify Tools                     | Security tools may be disabled or modified to reduce detection.                                             |
| Credential Access   | OS Credential Dumping - LSASS Memory        | Attackers may attempt to dump credentials from LSASS memory.                                                |
| Discovery           | Network Service Discovery                   | Network scanning may identify open services and possible movement paths.                                    |
| Discovery           | File and Directory Discovery                | Attackers may enumerate files and directories to find valuable data.                                        |
| Discovery           | Network Share Discovery                     | Network shares may be identified for data access or ransomware spread.                                      |
| Discovery           | System Network Configuration Discovery      | Attackers may check network configuration details.                                                          |
| Discovery           | System Information Discovery                | System information may be collected using WMI or command-line tools.                                        |
| Discovery           | Permission Groups Discovery - Domain Groups | Attackers may review group permissions to identify privileged accounts.                                     |
| Lateral Movement    | Remote Desktop Protocol                     | RDP may be used to move between systems.                                                                    |
| Lateral Movement    | Remote Access Software                      | Tools such as AnyDesk, Atera, ConnectWise, and Splashtop may support movement or access.                    |
| Lateral Movement    | Software Deployment Tools                   | PDQ Deploy and similar tools may be abused to push tools or payloads.                                       |
| Command and Control | Ingress Tool Transfer                       | Attackers may transfer tools into the environment.                                                          |
| Command and Control | Application Layer Protocol - Web Protocols  | Web-based communication may support attacker-controlled activity.                                           |
| Command and Control | Remote Access Software                      | Remote access tools may support command and control activity.                                               |
| Exfiltration        | Exfiltration Over Web Service               | Rclone may be used to exfiltrate data to cloud storage or remote services.                                  |
| Impact              | Data Encrypted for Impact                   | Files may be encrypted using the `.medusa` extension.                                                       |
| Impact              | Inhibit System Recovery                     | Shadow copies may be deleted to make recovery harder.                                                       |
| Impact              | Service Stop                                | Services related to backups, security, databases, communication, file sharing, and websites may be stopped. |
| Impact              | System Shutdown or Reboot                   | System disruption may occur during the ransomware impact phase.                                             |
| Impact              | Financial Theft                             | Ransomware creates financial pressure through extortion demands.                                            |

---

## 7. Indicators of Compromise

This report does not invent indicators. Any IOC should be copied only from trusted public reporting such as the CISA/FBI/MS-ISAC advisory or verified threat intelligence sources.

Suggested IOC tracking format:

| IOC Type       | IOC Value                   | Description                                                                                 | Source                          | Confidence |
| -------------- | --------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------- | ---------- |
| File Extension | `.medusa`                   | Extension used for encrypted files                                                          | CISA/FBI/MS-ISAC advisory notes | High       |
| File Name      | `gaze.exe`                  | Malware component associated with service termination, shadow copy deletion, and encryption | CISA/FBI/MS-ISAC advisory notes | High       |
| Tool           | Rclone                      | Used for data exfiltration                                                                  | CISA/FBI/MS-ISAC advisory notes | Medium     |
| Tool           | SoftPerfect Network Scanner | Used for discovery and scanning                                                             | CISA/FBI/MS-ISAC advisory notes | Medium     |
| Tool           | Ligolo                      | Reverse tunneling tool                                                                      | CISA/FBI/MS-ISAC advisory notes | Medium     |
| Tool           | Cloudflared                 | Tunneling or service exposure                                                               | CISA/FBI/MS-ISAC advisory notes | Medium     |

### Analyst Note

IOCs are useful for short-term detection and blocking. However, ransomware groups can change infrastructure, tools, filenames, and hashes. Because of this, defenders should combine IOC-based detection with TTP-based detection.

For example, detecting unusual Rclone activity, unexpected use of remote access tools, abnormal port scanning, suspicious PowerShell commands, or mass file encryption behavior may be more durable than only blocking a single IP address or hash.

---

## 8. Impact Assessment

A Medusa ransomware incident can affect an organization in several ways:

* Business disruption due to encrypted systems
* Loss of access to important files and applications
* Data theft before encryption
* Public exposure of sensitive information
* Recovery costs
* Legal and regulatory risk
* Reputational damage
* Pressure to pay ransom
* Extended downtime if backups are deleted, unavailable, or not tested

The use of double extortion increases the impact. Even if systems are restored from backup, stolen data may still create risk for the victim organization.

---

## 9. Defensive Recommendations

### 9.1 Identity and Access Security

* Require multifactor authentication for all users, especially administrator accounts, VPN access, remote access, and email.
* Audit user accounts regularly.
* Disable unused or inactive accounts.
* Review privileged accounts and domain group membership.
* Monitor unusual login activity, failed login spikes, and impossible travel patterns.
* Require VPNs or jump hosts for remote access.

### 9.2 Patch and Vulnerability Management

* Keep operating systems, software, and firmware up to date.
* Prioritize internet-facing systems.
* Patch known exploited vulnerabilities quickly.
* Review exposure of remote access tools and externally facing applications.
* Remove unsupported or outdated systems where possible.

### 9.3 Network Security

* Segment networks to limit lateral movement.
* Disable unused ports and services.
* Filter network traffic.
* Monitor unauthorized scanning and access attempts.
* Restrict RDP and remote administration access to approved users and systems only.

### 9.4 Monitoring and Detection

Security teams should monitor for:

* Unauthorized use of remote access tools
* Unusual PowerShell activity
* Suspicious Windows Command Prompt activity
* WMI usage from unusual accounts or hosts
* Certutil.exe usage for file transfers
* Rclone execution or unusual cloud upload behavior
* SoftPerfect Network Scanner activity
* Mass file changes or encryption-like behavior
* Attempts to delete shadow copies
* Attempts to stop backup, security, database, file sharing, or website services

### 9.5 Backup and Recovery

* Maintain offline or immutable backups.
* Test backup restoration regularly.
* Keep backups separated from domain administrator access.
* Ensure backup data is encrypted and protected.
* Create a recovery plan before an incident occurs.
* Monitor for attempts to delete shadow copies or stop backup services.

### 9.6 Hardening

* Disable unnecessary command-line and scripting permissions where possible.
* Restrict administrative tools to authorized IT staff.
* Review Active Directory permissions.
* Review domain controllers, servers, workstations, and critical systems.
* Limit software deployment tools to approved administrators.
* Maintain strong endpoint protection and logging.

---

## 10. Detection Opportunities

Based on the observed behavior, defenders can create detection logic around the following activities:

| Detection Area    | Example Activity to Monitor                                                                       |
| ----------------- | ------------------------------------------------------------------------------------------------- |
| Initial Access    | Suspicious logins, phishing-related account compromise, remote access from unusual locations      |
| Discovery         | Port scanning, network share enumeration, SoftPerfect Network Scanner usage                       |
| Command Execution | PowerShell, Windows Command Prompt, and WMI activity from unusual accounts                        |
| Defense Evasion   | Clearing command history, disabling security tools, suspicious Certutil usage                     |
| Lateral Movement  | RDP activity, unauthorized remote access tools, software deployment tool misuse                   |
| Exfiltration      | Rclone execution, large outbound data transfers, cloud storage uploads                            |
| Impact            | Service stopping, shadow copy deletion, mass file modification, `.medusa` file extension creation |

---

## 11. Analyst Takeaways

Medusa ransomware shows that modern ransomware defense must focus on the full attack lifecycle, not only the final encryption stage.

The most important takeaways are:

1. Initial access is often the most important phase to prevent. Phishing, stolen credentials, exposed services, and unpatched vulnerabilities create the entry points attackers need.
2. Living-off-the-land behavior makes detection harder because attackers may use normal tools such as PowerShell, WMI, Certutil, and remote access software.
3. Ransomware actors may steal data before encryption, which increases legal, financial, and reputational risk.
4. Backups must be offline, immutable, and tested because attackers may stop backup services and delete shadow copies.
5. Defenders should use both IOC-based and behavior-based detection. IOCs help with immediate response, while TTP-based detection is more useful when attacker infrastructure changes.

---

## 12. Conclusion

Medusa ransomware represents a serious threat because it combines initial access through phishing, brokers, or vulnerable systems with discovery, lateral movement, exfiltration, and encryption. The use of legitimate tools and remote access software makes detection more difficult, especially if organizations do not monitor administrative activity closely.

The strongest defensive approach is to reduce initial access opportunities, enforce MFA, patch exposed systems, monitor suspicious tool usage, segment networks, protect backups, and prepare an incident response plan.

This report helped convert a public ransomware advisory into a practical threat intelligence summary that can support SOC analysis, threat research, and defensive planning.

---

## References

1. [CISA/FBI/MS-ISAC Joint Cybersecurity Advisory - StopRansomware: Medusa Ransomware, AA25-071A](https://www.cisa.gov/sites/default/files/2025-03/aa25-071a-stopransomware-medusa-ransomware.pdf)
2. [MITRE ATT&CK Enterprise Matrix](https://attack.mitre.org/matrices/enterprise/)
3. CISA Known Exploited Vulnerabilities Catalog
4. VirusTotal Documentation
5. urlscan.io Documentation

---

## Disclaimer

This report is based only on publicly available information and personal study notes. It is intended for educational and portfolio purposes. It does not include private, leaked, or unauthorized data.
