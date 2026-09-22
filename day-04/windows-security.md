# Day 4 — Windows Security Fundamentals

## 🎯 Learning Goal

Understand the core security mechanisms in Windows and learn how defenders investigate users, permissions, processes, services, logs, firewall rules, RDP, and persistence.

By the end of Day 4, you should be able to:

- Understand Windows users and groups
- Understand NTFS permissions
- Understand UAC
- Inspect processes and services
- Use PowerShell for security enumeration
- Review Windows Event Logs
- Understand Windows Defender
- Review Windows Firewall
- Understand RDP security
- Inspect scheduled tasks
- Understand the Windows Registry from a security perspective
- Recognize basic privilege-escalation concepts

> ⚠️ Practice only on your own Windows machine or an authorized Windows evaluation VM.

---

## 1. Why Windows Security Matters

### 🇬🇧 English

Windows is widely used on desktops, laptops, enterprise networks, and Active Directory environments.

A compromised Windows account can become dangerous if the attacker can:

- Access sensitive files
- Execute malicious programs
- Abuse weak permissions
- Disable security controls
- Steal credentials
- Move to higher privileges
- Move to other systems

### 🇮🇳 Tinglish

Windows system lo attacker ki normal user access vachindani imagine cheyyi.

Direct ga Administrator avvakapovachu.

Attacker usually environment ni enumerate chesi weak permissions, credentials, services, scheduled tasks, or vulnerable software kosam search chestadu.

~~~text
Initial Access
     ↓
Enumeration
     ↓
Find Weakness
     ↓
Privilege Escalation
     ↓
Administrator / SYSTEM
~~~

Cybersecurity lo ee flow ni understand cheyyadam chala important.

---

## 2. Windows Users

Open Command Prompt or PowerShell.

Current user:

~~~powershell
whoami
~~~

More information:

~~~powershell
whoami /all
~~~

List local users:

~~~powershell
net user
~~~

### 🇮🇳 Tinglish

Linux lo whoami use chesinattu Windows lo kuda whoami use cheyochu.

whoami /all tho current user ki related:

- User identity
- Groups
- Privileges
- Security identifiers

lanti information chudachu.

Security question:

> **"Ee account ki unnecessary privileges unnaya?"**

---

## 3. Windows Groups

List local groups:

~~~powershell
net localgroup
~~~

Check members of Administrators:

~~~powershell
net localgroup Administrators
~~~

### 🇮🇳 Tinglish

Windows groups permissions manage cheyadaniki important.

Example:

~~~text
Administrators
    ├── User A
    └── User B
~~~

Administrators group lo unnecessary users unte attack impact increase avvachu.

Security principle:

> **Only required users should have administrative privileges.**

---

## 4. Windows Security Identifiers — SID

Windows identifies security principals using Security Identifiers (SIDs).

Run:

~~~powershell
whoami /user
~~~

You may see something similar to:

~~~text
S-1-5-21-...
~~~

### 🇮🇳 Tinglish

Username human-readable name.

SID Windows security system lo identity ni uniquely identify cheyadaniki use chestundi.

Simple ga:

> **Username = name**

> **SID = Windows security identity**

---

## 5. NTFS File Permissions

Windows uses NTFS permissions to control access to files and folders.

Check a folder:

~~~powershell
icacls C:\Users
~~~

Create a lab directory:

~~~powershell
mkdir $HOME\cyber-lab-day4
~~~

Check permissions:

~~~powershell
icacls $HOME\cyber-lab-day4
~~~

Common permissions include:

- Read
- Write
- Modify
- Full Control

### 🇮🇳 Tinglish

Linux lo rwx permissions chusam.

Windows lo NTFS permissions different model use chestundi.

Main question:

> **"Ee user/group ki ee file or folder meeda em access undi?"**

---

## 6. NTFS vs Share Permissions

For network shares, Windows can have both:

- Share permissions
- NTFS permissions

The effective access can be affected by both permission layers.

### 🇮🇳 Tinglish

Network share use chesthunappudu:

~~~text
User
 ↓
Share Permission
 ↓
NTFS Permission
 ↓
Effective Access
~~~

Kabatti share permission okay ani matrame chudakudadhu.

Actual NTFS permissions kuda review cheyali.

---

## 7. UAC — User Account Control

UAC helps prevent unauthorized changes by requiring elevation for actions that need administrative privileges.

You may see:

> **"Do you want to allow this app to make changes to your device?"**

### 🇮🇳 Tinglish

UAC ante Windows lo administrative action jaragadaniki additional confirmation/elevation mechanism.

Simple ga:

> **"Ee action ki admin privileges kavala?"**

ani Windows check chesi elevation prompt ivvachu.

UAC ni completely disable cheyyadam generally bad security practice.

---

## 8. Processes

List processes:

~~~powershell
Get-Process
~~~

Find a process:

~~~powershell
Get-Process | Where-Object {$_.ProcessName -like "*chrome*"}
~~~

Command Prompt alternative:

~~~cmd
tasklist
~~~

### 🇮🇳 Tinglish

Process ante currently run avtunna program instance.

Security analyst questions:

- Ee process enduku run avtundi?
- Ye user context lo run avtundi?
- Parent process enti?
- Unexpected process aa?
- Network connections unnaya?

Unknown process kanipiste immediately malware ani assume cheyyakunda investigate cheyali.

---

## 9. Windows Services

List services:

~~~powershell
Get-Service
~~~

Running services:

~~~powershell
Get-Service | Where-Object {$_.Status -eq "Running"}
~~~

### 🇮🇳 Tinglish

Windows service ante background lo run ayye system/application component.

Security perspective:

> **"Required kaani service run avtunda?"**

Unnecessary services attack surface increase cheyavachu.

---

## 10. Windows Firewall

Check firewall profiles:

~~~powershell
Get-NetFirewallProfile
~~~

List firewall rules:

~~~powershell
Get-NetFirewallRule | Select-Object DisplayName, Enabled, Direction, Action
~~~

### 🇬🇧 English

Windows Defender Firewall controls network traffic based on firewall rules.

### 🇮🇳 Tinglish

Firewall ni:

> **"Ee network traffic allow cheyali? Ee traffic block cheyali?"**

ani control chese security layer laga think cheyyi.

Important concepts:

- Inbound
- Outbound
- Allow
- Block
- Profile

---

## 11. Windows Defender

Check Microsoft Defender status:

~~~powershell
Get-MpComputerStatus
~~~

Useful information can include:

- Antivirus status
- Real-time protection
- Antispyware status
- Signature information

### 🇮🇳 Tinglish

Windows Defender system lo malware-related threats detect/prevent cheyadaniki important security control.

Security analyst ki questions:

> **"Real-time protection enabled ga unda?"**

> **"Security definitions updated ga unnaya?"**

---

## 12. Event Logs

Windows records many security-relevant events in Event Logs.

Open Event Viewer:

~~~text
Win + R
eventvwr.msc
~~~

Important areas include:

- Windows Logs → Security
- Windows Logs → System
- Windows Logs → Application

### 🇮🇳 Tinglish

Event Logs ante Windows lo jarigina important events ki records.

Security investigation lo logs chala important.

Example questions:

> Evaru login ayyadu?

> Failed login attempts unnaya?

> Service eppudu start/stop ayyindi?

> System lo suspicious event jariginda?

---

## 13. Security Event Log

PowerShell tho recent Security events chudachu:

~~~powershell
Get-WinEvent -LogName Security -MaxEvents 20
~~~

Common examples:

| Event ID | Meaning |
|---:|---|
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4634 | Logoff |
| 4648 | Logon using explicit credentials |
| 4672 | Special privileges assigned to new logon |

> Event interpretation depends on the event context. Do not treat one event alone as proof of malicious activity.

### 🇮🇳 Tinglish

Example:

4625 repeated ga kanipisthe failed login attempts jarigayi ani clue.

But:

> **Single event chusi attacker ani decide cheyyakudadhu.**

Context, username, source system, timing, and other events kuda investigate cheyali.

---

## 14. PowerShell Security

PowerShell is a powerful Windows administration and automation tool.

Check version:

~~~powershell
$PSVersionTable
~~~

Find command information:

~~~powershell
Get-Command Get-Process
~~~

### 🇮🇳 Tinglish

PowerShell normal administration ki kuda use chestaru, security investigation ki kuda use chestaru.

Cybersecurity lo PowerShell important because:

- System information collect cheyochu
- Processes inspect cheyochu
- Services inspect cheyochu
- Logs query cheyochu
- Security configuration review cheyochu

PowerShell command kanipinchindi ante automatic ga malicious ani assume cheyyakudadhu.

---

## 15. Scheduled Tasks

Windows Scheduled Tasks can execute programs at specific times or events.

List tasks:

~~~powershell
Get-ScheduledTask
~~~

Find running tasks:

~~~powershell
Get-ScheduledTask | Where-Object {$_.State -eq "Running"}
~~~

### 🇮🇳 Tinglish

Linux lo cron jobs chusam.

Windows lo similar concept:

> **Scheduled Tasks**

Security perspective lo unknown task enduku create ayyindo investigate cheyali.

Attackers persistence kosam scheduled tasks abuse cheyyagalru.

---

## 16. Windows Registry

The Windows Registry stores configuration information used by Windows and applications.

Open Registry Editor:

~~~text
Win + R
regedit
~~~

Important security concept:

> Registry is sensitive system configuration data.

### 🇮🇳 Tinglish

Registry ni Windows operating system ki oka huge configuration database laga imagine cheyochu.

Registry lo random changes cheyyakudadhu.

Basic learning stage lo:

> **Read and understand first. Don't modify unknown keys.**

---

## 17. RDP Security

Remote Desktop Protocol (RDP) allows remote graphical access to Windows systems.

Security concerns include:

- Exposed RDP
- Weak passwords
- Excessive user access
- Missing network restrictions
- Outdated systems
- Brute-force attempts

### 🇮🇳 Tinglish

RDP ante remote ga Windows desktop ni access cheyadaniki use chestam.

Security question:

> **"RDP actually required aa?"**

Required ayithe:

- Strong authentication
- Limited access
- Network restrictions
- Monitoring
- Updates

important.

---

## 18. Windows Credential Security

Windows systems can contain sensitive credentials and authentication material.

Examples include:

- Passwords
- Access tokens
- Stored credentials
- Service account credentials

### 🇮🇳 Tinglish

Credentials attacker ki dorikithe normal account access kanna much bigger impact ravachu.

So:

> **Credentials ni unnecessary ga files, scripts, registry entries, or command history lo store cheyyakudadhu.**

---

## 19. Basic Windows Privilege Escalation Concept

Privilege escalation means moving from a lower privilege context to a higher privilege context.

Typical areas defenders should review:

- Weak file permissions
- Weak service permissions
- Excessive local administrator access
- Vulnerable software
- Misconfigured scheduled tasks
- Insecure credentials
- Dangerous registry configuration
- Unpatched systems

### 🇮🇳 Tinglish

Normal user account compromise ayyaka attacker:

~~~text
Normal User
     ↓
Enumeration
     ↓
Find Misconfiguration
     ↓
Exploit Weakness
     ↓
Administrator / SYSTEM
~~~

Defender goal:

> **Ee escalation path available undakunda permissions and configurations secure cheyadam.**

---

## 20. Windows Security Checklist

~~~text
[ ] Identify current user
[ ] Review local users
[ ] Review Administrators group
[ ] Review NTFS permissions
[ ] Check UAC
[ ] Review running processes
[ ] Review services
[ ] Check firewall profiles
[ ] Review Defender status
[ ] Review Security Event Logs
[ ] Review scheduled tasks
[ ] Understand RDP exposure
[ ] Review sensitive credential storage
[ ] Apply least privilege
[ ] Keep Windows and software updated
~~~

---

# 🧪 Day 4 Hands-on Lab

Perform these on your own Windows machine or Windows VM.

### User Enumeration

~~~powershell
whoami
whoami /all
net user
net localgroup Administrators
~~~

### File Permission Lab

~~~powershell
mkdir $HOME\cyber-lab-day4
icacls $HOME\cyber-lab-day4
~~~

### Process Enumeration

~~~powershell
Get-Process
tasklist
~~~

### Service Enumeration

~~~powershell
Get-Service
Get-Service | Where-Object {$_.Status -eq "Running"}
~~~

### Firewall Review

~~~powershell
Get-NetFirewallProfile
~~~

### Defender Review

~~~powershell
Get-MpComputerStatus
~~~

### Event Log Review

~~~powershell
Get-WinEvent -LogName Security -MaxEvents 20
~~~

### Scheduled Tasks

~~~powershell
Get-ScheduledTask
~~~

---

# 🎯 Day 4 Mini Challenge

Without modifying security settings, answer these questions:

1. Which Windows user are you currently using?
2. Is your account a member of Administrators?
3. What permissions does your lab folder have?
4. How many running processes can you identify?
5. Which important services are running?
6. Is Windows Firewall enabled for the active profile?
7. Is Microsoft Defender active?
8. Can you find successful and failed logon events?
9. What scheduled tasks exist?
10. Is RDP enabled on your lab VM?
11. What security controls would you check after a suspicious login?

Write your observations in your notes.

---

# 🎤 Interview Questions

### Q1. What is UAC?

**English:** User Account Control helps prevent unauthorized administrative changes by requiring elevation or confirmation for certain actions.

**Tinglish:** Administrative privileges required ayye actions ki Windows additional elevation/confirmation provide cheyadaniki UAC use chestundi.

### Q2. What is NTFS permission?

**English:** NTFS permissions control access to files and folders for users and groups.

**Tinglish:** Windows files/folders ni e user or group read, write, modify, or fully control cheyagalro NTFS permissions decide chestayi.

### Q3. What is Windows Event Viewer?

**English:** Event Viewer is a Windows interface for viewing system, application, and security event logs.

**Tinglish:** Windows lo jarigina important events and security activities ni logs form lo chudataniki Event Viewer use chestam.

### Q4. What is Windows Defender?

**English:** Microsoft Defender provides built-in security capabilities including antivirus and threat protection.

**Tinglish:** Windows system ni malware and other threats nunchi protect cheyadaniki Defender important built-in security control.

### Q5. What is privilege escalation?

**English:** Privilege escalation is obtaining higher privileges than originally authorized.

**Tinglish:** Normal user access nunchi Administrator or SYSTEM level privileges ki move avvadam privilege escalation.

### Q6. Why are Windows Event Logs important?

**English:** Logs provide evidence that can help detect, investigate, and reconstruct security events.

**Tinglish:** Login attempts, process/service activity, and other events ni investigate cheyadaniki logs important evidence provide chestayi.

---

# 🧠 Day 4 Summary

~~~text
Windows Users & Groups
          ↓
SIDs
          ↓
NTFS Permissions
          ↓
UAC
          ↓
Processes
          ↓
Services
          ↓
Firewall
          ↓
Defender
          ↓
Event Logs
          ↓
PowerShell
          ↓
Scheduled Tasks
          ↓
RDP
          ↓
Privilege Escalation
~~~

## 🇮🇳 Final Tinglish Memory

> **Windows Security ante users/groups evaru, vallaki em permissions unnayi, em processes/services run avtunnayi, firewall and Defender active ga unnaya, logs em cheptunnayi, scheduled tasks enti, RDP exposure unda ani continuously review chesi unnecessary access ni reduce cheyadam.**

**Next:** Day 5 — Cryptography Fundamentals.
