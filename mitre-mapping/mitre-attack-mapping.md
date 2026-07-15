# MITRE ATT&CK Mapping - Medusa Ransomware

| Tactic | Technique / Behavior | Explanation |
|---|---|---|
| Initial Access | Phishing | Phishing may be used to trick users into opening malicious content or giving away credentials. |
| Initial Access | Exploit Public-Facing Application | Unpatched software vulnerabilities may be exploited to gain access. |
| Initial Access | Initial Access Brokers | Access may be obtained through brokers who provide entry into victim environments. |
| Execution | PowerShell | PowerShell may be used for command execution and system activity. |
| Execution | Windows Command Shell | Windows command shell may be used for execution and enumeration. |
| Execution | Windows Management Instrumentation | WMI may be used to query systems or support remote activity. |
| Persistence | Create Account | Attackers may create accounts to maintain access. |
| Defense Evasion | Clear Command History | Clearing history may remove traces of attacker activity. |
| Defense Evasion | Obfuscated or Encrypted Files | Obfuscation can make analysis and detection harder. |
| Defense Evasion | Disable or Modify Tools | Security tools may be disabled or modified to reduce detection. |
| Credential Access | OS Credential Dumping - LSASS Memory | Attackers may attempt to dump credentials from LSASS memory. |
| Discovery | Network Service Discovery | Network scanning may identify open services and possible movement paths. |
| Discovery | File and Directory Discovery | Attackers may enumerate files and directories to find valuable data. |
| Discovery | Network Share Discovery | Network shares may be identified for data access or ransomware spread. |
| Discovery | System Network Configuration Discovery | Attackers may check network configuration details. |
| Discovery | System Information Discovery | System information may be collected using WMI or command-line tools. |
| Discovery | Permission Groups Discovery - Domain Groups | Attackers may review group permissions to identify privileged accounts. |
| Lateral Movement | Remote Desktop Protocol | RDP may be used to move between systems. |
| Lateral Movement | Remote Access Software | Tools such as AnyDesk, Atera, ConnectWise, and Splashtop may support movement or access. |
| Lateral Movement | Software Deployment Tools | PDQ Deploy and similar tools may be abused to push tools or payloads. |
| Command and Control | Ingress Tool Transfer | Attackers may transfer tools into the environment. |
| Command and Control | Application Layer Protocol - Web Protocols | Web-based communication may support attacker-controlled activity. |
| Command and Control | Remote Access Software | Remote access tools may support command and control activity. |
| Exfiltration | Exfiltration Over Web Service | Rclone may be used to exfiltrate data to cloud storage or remote services. |
| Impact | Data Encrypted for Impact | Files may be encrypted using the `.medusa` extension. |
| Impact | Inhibit System Recovery | Shadow copies may be deleted to make recovery harder. |
| Impact | Service Stop | Services related to backups, security, databases, communication, file sharing, and websites may be stopped. |
| Impact | System Shutdown or Reboot | System disruption may occur during the ransomware impact phase. |
| Impact | Financial Theft | Ransomware creates financial pressure through extortion demands. |

## Analyst Note

This mapping is based on publicly available reporting and study notes. Exact technique IDs may vary depending on the evidence available in a specific incident.
