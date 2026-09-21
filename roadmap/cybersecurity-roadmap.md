# Pure Cybersecurity Roadmap

This repository is a hands-on learning journey focused on **core cybersecurity** rather than DevSecOps or cloud engineering.

## Learning Philosophy

Every topic follows:

```text
Concept
  ↓
How the technology works
  ↓
Security weakness
  ↓
Authorized lab
  ↓
Detection
  ↓
Remediation
  ↓
Documentation
```

All offensive security practice must be performed only against systems you own or have explicit permission to test.

## Phase 1 — Cybersecurity Fundamentals
- CIA Triad
- Threats, vulnerabilities, risks
- Attack surface
- Security controls
- Authentication and authorization
- Defense in depth
- Least privilege
- Common attack types

## Phase 2 — Networking Fundamentals
- OSI and TCP/IP
- IPv4/IPv6
- MAC, ARP, TCP, UDP, ICMP
- DNS, DHCP
- HTTP/HTTPS and TLS
- SSH, SMTP, FTP/SFTP
- Routing, NAT, VLANs
- Proxies, firewalls, VPNs
- Network segmentation

Tools: Wireshark, tcpdump, Nmap, Netcat, dig, nslookup, curl.

## Phase 3 — Linux Security
- Users, groups, permissions
- SUID/SGID
- Processes and services
- Systemd
- SSH security
- Cron
- Logs
- Linux capabilities
- sudo
- File integrity
- Hardening

Tools: grep, awk, sed, ps, ss, lsof, journalctl, find, chmod, chown, strace.

## Phase 4 — Windows Security
- Windows architecture
- Users/groups
- NTFS permissions
- Services and Registry
- PowerShell
- Event Logs
- Defender and Firewall
- UAC
- Credential storage
- Active Directory
- Group Policy

Tools: PowerShell, Event Viewer, Sysinternals, BloodHound in authorized labs.

## Phase 5 — Cryptography
- Symmetric/asymmetric encryption
- Hashing and password hashing
- Digital signatures
- Certificates and PKI
- TLS
- Key management
- Encoding vs encryption vs hashing

Algorithms: AES, RSA, ECC, SHA-2, SHA-3, HMAC, bcrypt, scrypt, Argon2.

## Phase 6 — Identity & Access Security
- Authentication
- Authorization
- Sessions and cookies
- MFA
- OAuth
- OpenID Connect
- SAML
- Kerberos
- LDAP
- Active Directory
- Privileged accounts

## Phase 7 — Web Application Security
- HTTP
- Headers
- Cookies and sessions
- REST APIs
- Authentication flows
- Same-Origin Policy
- CORS
- JWT
- OWASP Top 10
- Burp Suite
- OWASP ZAP

## Phase 8 — Vulnerability Assessment
- Asset discovery
- Reconnaissance
- Enumeration
- Service identification
- CVE and CVSS
- Vulnerability validation
- Risk assessment
- Reporting
- Remediation verification

Tools: Nmap, Nuclei, OpenVAS/Greenbone, Nessus concepts, SearchSploit.

## Phase 9 — Ethical Hacking & Penetration Testing
- Passive and active reconnaissance
- DNS/subdomain enumeration
- Port and service enumeration
- Vulnerability exploitation in controlled labs
- Privilege escalation
- Credential discovery
- Lateral movement concepts
- Reporting

## Phase 10 — Active Directory Security
- Domains, forests and trusts
- Domain Controllers
- Kerberos, NTLM, LDAP
- SPNs
- Delegation
- Privileged groups
- Kerberoasting
- AS-REP roasting
- Pass-the-Hash concepts
- Attack-path analysis
- Detection and remediation

## Phase 11 — SOC & Defensive Security
- Alert triage
- Event analysis
- Log analysis
- Detection engineering
- IOC analysis
- Threat hunting
- Security monitoring

Logs: Windows, Linux, web, DNS, firewall, proxy and endpoint telemetry.

## Phase 12 — SIEM
- Log ingestion
- Parsing and normalization
- Correlation
- Alerting
- Dashboards
- Detection rules
- False positives
- Investigation

Platforms: Splunk, Elastic Security, Microsoft Sentinel concepts, Wazuh.

## Phase 13 — Incident Response
- Preparation
- Identification
- Containment
- Eradication
- Recovery
- Lessons learned

Practice investigating suspicious logins, malware alerts, brute force, web attacks, exfiltration indicators and compromised endpoints.

## Phase 14 — Digital Forensics
- Evidence handling
- Chain of custody
- Disk forensics
- Memory forensics
- File-system artifacts
- Browser artifacts
- Windows/Linux artifacts
- Timeline analysis

Tools: Autopsy, Volatility, FTK concepts, Plaso/log2timeline.

## Phase 15 — Malware Analysis
- Malware types and lifecycle
- Static analysis
- Dynamic analysis
- IOCs
- Persistence
- Command and control
- Sandboxing
- PE files
- Assembly basics
- Debugging
- Reverse engineering

Tools: Ghidra, x64dbg, Detect It Easy, Strings, YARA, Procmon.

## Phase 16 — Threat Intelligence
- Threat actors
- TTPs
- IOCs/IOAs
- Threat feeds
- Malware intelligence
- Campaign analysis
- MITRE ATT&CK

## Phase 17 — Network Security
- Firewalls
- IDS/IPS
- Network segmentation
- VPN
- Proxy security
- Network monitoring
- Packet analysis
- Attack detection

Tools: Wireshark, Zeek, Suricata, Snort.

## Phase 18 — Red Team & Blue Team
### Red Team
- Recon
- Enumeration
- Initial access
- Privilege escalation
- Lateral movement
- Persistence concepts
- C2 concepts
- Reporting

### Blue Team
- Detection
- Monitoring
- Threat hunting
- Incident response
- Forensics
- Remediation

### Purple Team
Connect attacks to detections, investigations, remediation and improved detection.

## Phase 19 — Security Architecture
- Defense in depth
- Network segmentation
- Identity architecture
- Secure authentication
- Security controls
- Threat modeling
- Attack surface management
- Secure system design
- Risk management

## Phase 20 — Advanced Cybersecurity
- Advanced Active Directory security
- Advanced web exploitation
- Binary exploitation fundamentals
- Reverse engineering
- Advanced malware analysis
- Threat hunting
- Detection engineering
- Adversary simulation
- Security research
- Vulnerability research

## Practice Environment

```text
Cybersecurity Lab
│
├── Kali Linux
├── Ubuntu
├── Windows evaluation VM
├── OWASP Juice Shop
├── DVWA
├── WebGoat
├── Metasploitable
├── Wazuh
└── Wireshark
```

Practice only against intentionally vulnerable systems and systems you own or are explicitly authorized to test.

## Suggested Learning Order

```text
Fundamentals → Networking → Linux → Windows
→ Cryptography → Identity & Access → Web Security
→ Vulnerability Assessment → Ethical Hacking
→ Active Directory → SOC → SIEM
→ Incident Response → Forensics → Malware Analysis
→ Threat Intelligence → Red Team + Blue Team
→ Advanced Security
```

## Current Progress

- [x] Day 1 — Cybersecurity Fundamentals
- [x] Day 2 — Networking, Ports & Nmap
- [ ] Day 3 — Linux Security
- [ ] Day 4 — Linux Permissions & Users
- [ ] Day 5 — Processes, Services & Logs
- [ ] Day 6 — Windows Security
- [ ] Day 7 — Windows Event Logs
- [ ] Continue...
