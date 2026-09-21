# Day 3 — Linux Security

## 🎯 Learning Goal

Understand how Linux controls users, permissions, processes, services, SSH access, scheduled jobs, and logs.

By the end of Day 3, you should be able to:

- Identify users and groups
- Understand Linux file permissions
- Use chmod, chown, and sudo
- Understand SUID and SGID
- Inspect running processes and services
- Review SSH security basics
- Identify cron jobs
- Find important Linux logs
- Understand the basics of privilege escalation
- Perform basic Linux security checks

> ⚠️ Practice only on your own Linux machine or an intentionally vulnerable lab VM.

---

## 1. Why Linux Security Matters

### 🇬🇧 English

Linux is widely used for servers, applications, containers, security tools, and infrastructure.

An attacker who gains a low-privileged Linux account may try to:

1. Discover the environment
2. Find credentials or secrets
3. Identify vulnerable services
4. Abuse weak permissions
5. Escalate privileges
6. Maintain access

### 🇮🇳 Tinglish

Linux server lo attacker ki normal user access vachindani imagine cheyyi.

Appudu attacker direct ga root avvakapovachu.

Usually first:

~~~text
Initial Access
     ↓
Enumeration
     ↓
Find Weakness
     ↓
Privilege Escalation
     ↓
Root / Higher Privilege
~~~

Kabatti Linux security lo **users, permissions, processes, services, credentials, logs** chala important.

---

## 2. Users

Check current user:

~~~bash
whoami
~~~

More information:

~~~bash
id
~~~

List users:

~~~bash
cat /etc/passwd
~~~

### 🇮🇳 Tinglish

whoami ante:

> **"Ippudu nenu ye user tho login ayyanu?"**

id command user ID and group information chupistundi.

---

## 3. /etc/passwd

View:

~~~bash
cat /etc/passwd
~~~

A simplified entry looks like:

~~~text
username:x:1000:1000:User Name:/home/username:/bin/bash
~~~

Important fields:

~~~text
username
password placeholder
UID
GID
comment
home directory
login shell
~~~

### 🇮🇳 Tinglish

/etc/passwd lo system users gurinchi information untundi.

Important point:

> Modern Linux systems lo actual password hashes normally /etc/passwd lo store cheyaru.

---

## 4. /etc/shadow

Check permissions:

~~~bash
ls -l /etc/shadow
~~~

On a normal Linux system, access to this file is highly restricted.

### 🇮🇳 Tinglish

/etc/shadow lo password-related hashes and account password-aging information untayi.

Idi sensitive file.

Simple rule:

> **Password hashes unna file ni unnecessary users read cheyakudadhu.**

Don't modify it during the basic lab.

---

## 5. Users and Groups

Check your groups:

~~~bash
groups
~~~

List local groups:

~~~bash
cat /etc/group
~~~

### 🇮🇳 Tinglish

Group ante multiple users ni oka permission boundary lo organize cheyadaniki use chestaru.

Example:

~~~text
developers
   ├── user1
   ├── user2
   └── user3
~~~

Group ki file access permission unte aa group members ki access ravachu.

---

## 6. Linux File Permissions

Create a test file:

~~~bash
touch security-test.txt
ls -l security-test.txt
~~~

Example:

~~~text
-rw-r--r--  1 user group 0 security-test.txt
~~~

Breakdown:

~~~text
- rw- r-- r--
  │   │   │
  │   │   └── Others
  │   └────── Group
  └────────── Owner
~~~

Permissions:

- r = read
- w = write
- x = execute

### 🇮🇳 Tinglish

Linux lo file ki:

> **Evaru read cheyagalru? Evaru modify cheyagalru? Evaru execute cheyagalru?**

ani permissions decide chestayi.

---

## 7. Numeric Permissions

Common values:

~~~text
r = 4
w = 2
x = 1
~~~

Examples:

~~~text
7 = rwx
6 = rw-
5 = r-x
4 = r--
0 = ---
~~~

Therefore:

~~~text
755 = rwx r-x r-x
644 = rw- r-- r--
700 = rwx --- ---
600 = rw- --- ---
~~~

### 🇮🇳 Tinglish

755 ni:

~~~text
Owner  → rwx
Group  → r-x
Others → r-x
~~~

ani read cheyyali.

---

## 8. chmod

Change permissions:

~~~bash
chmod 600 security-test.txt
ls -l security-test.txt
~~~

Restore a common non-executable file permission:

~~~bash
chmod 644 security-test.txt
~~~

### 🇮🇳 Tinglish

chmod ante:

> **Change Mode**

File ki permissions change cheyadaniki use chestam.

Security perspective:

> Sensitive file ki unnecessary write permission ivvakudadhu.

---

## 9. chown

Check ownership:

~~~bash
ls -l security-test.txt
~~~

Change ownership only when you understand the effect and have appropriate privileges.

Example syntax:

~~~bash
sudo chown username:group security-test.txt
~~~

### 🇮🇳 Tinglish

chown ante:

> **Change Owner**

Wrong ownership valla application or system files ki unexpected access ravachu.

---

## 10. sudo

Check sudo privileges:

~~~bash
sudo -l
~~~

### 🇬🇧 English

sudo allows an authorized user to run commands with another user's privileges, commonly root.

### 🇮🇳 Tinglish

sudo ante simple ga:

> **"Na normal user privileges kanna higher privileges tho ee command run cheyyacha?"**

ani system check chesi command execute cheyadaniki use chestundi.

Security risk:

If a user has unnecessarily broad sudo permissions, an attacker who compromises that account may gain a path to higher privileges.

---

## 11. Root

Root is the traditional Linux superuser.

Check:

~~~bash
id
~~~

If you see:

~~~text
uid=0(root)
~~~

you are root.

### 🇮🇳 Tinglish

Root ki system lo extremely high privileges untayi.

So security principle:

> **Use least privilege.**

Normal work ki root account use cheyyadam avoid cheyyali.

---

## 12. SUID

SUID means **Set User ID**.

Find SUID files on your own lab system:

~~~bash
find / -perm -4000 -type f 2>/dev/null
~~~

### 🇬🇧 English

When an executable has the SUID permission, it can execute with the effective user ID of the file owner.

If the owner is root, that executable may run with root-level effective privileges.

### 🇮🇳 Tinglish

Normal ga file ni execute chesthe mana user permissions tho run avtundi.

SUID unte:

> **File owner permissions tho executable run avvachu.**

Root-owned SUID programs therefore deserve careful security review.

⚠️ Don't exploit random SUID binaries. First learn to identify and understand them in your own lab.

---

## 13. SGID

SGID means **Set Group ID**.

Find SGID files:

~~~bash
find / -perm -2000 -type f 2>/dev/null
~~~

### 🇮🇳 Tinglish

SGID executable group permissions tho related behavior provide chestundi.

Directories meeda SGID use chesthe, new files generally directory's group inheritance behavior follow chestayi.

Security lo unexpected group permissions identify cheyadaniki idi useful.

---

## 14. Processes

List processes:

~~~bash
ps aux
~~~

Interactive view:

~~~bash
top
~~~

Find a process:

~~~bash
ps aux | grep ssh
~~~

### 🇮🇳 Tinglish

Process ante currently system lo run avtunna program instance.

Security perspective:

> **Unknown process enduku run avtundi? E user tho run avtundi? E files/network connections use chestundi?**

ani investigate cheyyali.

---

## 15. Services

On systems using systemd:

~~~bash
systemctl --type=service --state=running
~~~

Check a service:

~~~bash
systemctl status ssh
~~~

Service listening ports can also be reviewed with:

~~~bash
ss -tulpn
~~~

### 🇮🇳 Tinglish

Service ante background lo continuously run ayye system/application component.

Example:

~~~text
SSH Service
     ↓
Port 22
     ↓
Remote Login
~~~

Security question:

> **"Ee service actually required aa?"**

Required kaakapothe unnecessary attack surface create avvachu.

---

## 16. SSH Security Basics

SSH commonly uses port 22.

Important security concepts:

- Prefer strong authentication
- Use SSH keys where appropriate
- Disable unnecessary accounts
- Avoid direct root login where not required
- Restrict access to trusted users/networks
- Keep SSH software updated
- Review authentication logs

### 🇮🇳 Tinglish

SSH remote login kosam use chestam.

Basic security mindset:

> "Evaru SSH login cheyagalru?"

> "Root direct login avasaram unda?"

> "Password authentication required aa?"

> "Failed login attempts unnaya?"

---

## 17. Cron Jobs

Cron is used for scheduled tasks.

List your cron jobs:

~~~bash
crontab -l
~~~

System cron locations can include:

~~~text
/etc/crontab
/etc/cron.d/
/etc/cron.daily/
/etc/cron.hourly/
~~~

### 🇮🇳 Tinglish

Cron ante:

> **"Ee command ni scheduled time lo automatically run cheyyi."**

Security perspective:

Attacker persistence kosam scheduled tasks abuse cheyyadaniki try cheyochu.

So unknown scheduled jobs investigate cheyyali.

---

## 18. Linux Logs

Common log locations:

~~~text
/var/log/
/var/log/auth.log
/var/log/secure
~~~

The exact files depend on the Linux distribution.

On systemd systems:

~~~bash
journalctl
~~~

Authentication-related logs:

~~~bash
journalctl | grep -i ssh
~~~

### 🇮🇳 Tinglish

Logs ante system lo jarigina events ki records.

Security team logs use chesi:

- Failed login attempts
- Successful logins
- Service failures
- Suspicious activity

identify cheyagalru.

---

## 19. Basic Privilege Escalation Concept

Privilege escalation means moving from a lower privilege level to a higher privilege level.

Example:

~~~text
Normal User
     ↓
Find Weak Permission
     ↓
Abuse Misconfiguration
     ↓
Higher Privilege
     ↓
Root
~~~

### Common areas defenders should review

- Weak file permissions
- Excessive sudo permissions
- Dangerous SUID binaries
- Vulnerable software
- Exposed credentials
- Unsafe scheduled jobs
- Misconfigured services
- Weak authentication

### 🇮🇳 Tinglish

Privilege escalation ante:

> **Normal user access nunchi higher privilege, usually root, ki move avvadam.**

Defender perspective lo goal:

> **"Ee path attacker ki available unda?"**

ani identify chesi remove cheyadam.

---

## 20. Least Privilege

Least privilege means giving users and processes only the permissions they actually need.

### 🇮🇳 Tinglish

User ki required permission matrame ivvali.

Example:

~~~text
Read-only task
    ↓
Read permission

Admin task
    ↓
Admin permission
~~~

Every user ki root access ivvadam bad security practice.

---

## 21. Linux Security Checklist

Use this checklist during a basic security review:

~~~text
[ ] Identify users
[ ] Review groups
[ ] Review sensitive file permissions
[ ] Check sudo privileges
[ ] Check SUID/SGID files
[ ] Review running processes
[ ] Review running services
[ ] Check listening ports
[ ] Review SSH configuration
[ ] Review cron jobs
[ ] Review authentication logs
[ ] Remove unnecessary services
[ ] Apply least privilege
[ ] Keep software updated
~~~

---

# 🧪 Day 3 Hands-on Lab

Perform these commands on your own Linux VM.

### User Enumeration

~~~bash
whoami
id
groups
cat /etc/passwd
~~~

### Permission Lab

~~~bash
mkdir -p ~/cyber-lab/day3
cd ~/cyber-lab/day3
touch security-test.txt
ls -l security-test.txt
chmod 600 security-test.txt
ls -l security-test.txt
chmod 644 security-test.txt
ls -l security-test.txt
~~~

### Process & Service Enumeration

~~~bash
ps aux
ss -tulpn
~~~

If systemd is available:

~~~bash
systemctl --type=service --state=running
~~~

### SUID / SGID Enumeration

~~~bash
find / -perm -4000 -type f 2>/dev/null
find / -perm -2000 -type f 2>/dev/null
~~~

### Cron Review

~~~bash
crontab -l
~~~

### Logs

On a systemd Linux VM:

~~~bash
journalctl -n 50
journalctl | grep -i ssh
~~~

---

# 🎯 Day 3 Mini Challenge

Without changing system configuration, answer these questions on your Linux VM:

1. Which user are you currently using?
2. What groups does your user belong to?
3. What permissions does your test file have?
4. Which processes are running?
5. Which network ports are listening?
6. Which services are running?
7. Are there any SUID files?
8. Are there any SGID files?
9. What cron jobs does your user have?
10. Where can authentication events be found?

Write your observations in your own notes.

---

# 🎤 Interview Questions

### Q1. What are Linux file permissions?

**English:** Linux file permissions control read, write, and execute access for the owner, group, and others.

**Tinglish:** File ni evaru read, write, execute cheyagalro permissions decide chestayi.

### Q2. What is chmod?

**English:** chmod changes file or directory permissions.

**Tinglish:** chmod file permissions change cheyadaniki use chestam.

### Q3. What is chown?

**English:** chown changes the owner and/or group ownership of a file.

**Tinglish:** File owner or group ownership change cheyadaniki chown use chestam.

### Q4. What is SUID?

**English:** SUID allows an executable to run with the effective user ID of its owner.

**Tinglish:** SUID executable owner permissions tho run avvadaniki allow chestundi.

### Q5. What is privilege escalation?

**English:** Privilege escalation is obtaining higher privileges than originally authorized.

**Tinglish:** Normal user access nunchi higher privilege, usually root, ki move avvadam privilege escalation.

### Q6. Why is least privilege important?

**English:** It limits the impact of compromised accounts and reduces unnecessary access.

**Tinglish:** Account compromise ayina damage limited ga undadaniki required permissions matrame ivvali.

---

# 🧠 Day 3 Summary

~~~text
Users & Groups
      ↓
File Permissions
      ↓
chmod / chown
      ↓
sudo / Root
      ↓
SUID / SGID
      ↓
Processes
      ↓
Services
      ↓
SSH
      ↓
Cron
      ↓
Logs
      ↓
Privilege Escalation
      ↓
Linux Hardening
~~~

## 🇮🇳 Final Tinglish Memory

> **Linux Security ante users evaru, vallaki em permissions unnayi, em processes/services run avtunnayi, em ports open unnayi, scheduled jobs enti, logs em cheptunnayi ani understand chesi unnecessary access ni reduce cheyadam.**

**Next:** Day 4 — Windows Security Fundamentals.
