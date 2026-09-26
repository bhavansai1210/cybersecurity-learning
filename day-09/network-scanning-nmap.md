# Day 9 — Network Scanning & Nmap

## 🎯 Learning Goal
Understand network scanning methodology and use Nmap to identify hosts, ports, services, versions, and security-relevant exposure in an authorized lab.

The syllabus covers host discovery, port scanning, TCP/UDP scanning, service enumeration, version detection, OS detection, Nmap scan types, network mapping, vulnerable-service identification, and scan-result analysis. fileciteturn16file0

> ⚠️ Scan only localhost, your own lab, or systems where you have explicit permission.

## 1. What is Network Scanning?
Network scanning identifies reachable hosts, open ports, and services.
Host Discovery → Port Scanning → Service Enumeration → Version Detection → Security Analysis
**🇮🇳 Tinglish:** Ee network/system lo em active ga undi? Ye ports open unnayi? Ye services run avtunnayi? ani understand cheyadam.

## 2. Host Discovery
    nmap -sn 127.0.0.1
Authorized lab subnet example:
    nmap -sn 192.168.56.0/24
Replace the subnet with your actual isolated lab subnet.

## 3. Port Scanning
    nmap 127.0.0.1
    nmap -p 22,80,443 127.0.0.1
    nmap -p 1-1000 127.0.0.1
**🇮🇳 Tinglish:** Port ni oka door laga imagine cheyyi. Open port ante service accessible undochu.

## 4. TCP vs UDP Scanning
    nmap -sU -p 53 127.0.0.1
UDP scans can be slower and interpretation differs from TCP.
**🇮🇳 Tinglish:** DNS commonly uses UDP, so TCP matrame scan chesthe complete picture ravakapovachu.

## 5. Service Enumeration
    nmap -sV 127.0.0.1
**🇮🇳 Tinglish:** Open port venaka actual service enti, possible ayithe version enti ani identify cheyadam.

## 6. OS Detection
    sudo nmap -O 127.0.0.1
OS detection is an estimate and is not always accurate.

## 7. Save Results
    nmap -sV -oN day9-scan.txt 127.0.0.1

## 8. Reading Output
Typical format:
    PORT     STATE    SERVICE
    22/tcp   open     ssh
    80/tcp   open     http
    443/tcp  open     https
Understand port, state, service, and version when detected.

## 9. Security Perspective
For every open port ask:
1. Why is it open?
2. What service is behind it?
3. Is it required?
4. Is it exposed to the correct network?
5. Is it patched?
6. Does it require authentication?
7. Is access logged?
8. Is encryption used?
**🇮🇳 Tinglish:** Open port itself automatically vulnerability kaadu. Why is it exposed? ane question important.

## 10. Scanning Methodology
Define Scope → Discover Hosts → Scan Ports → Enumerate Services → Identify Versions → Review Exposure → Validate → Document

## 11. DevSecOps Connection
Security validation can be added to controlled test environments:
Build → Security Tests → Deploy to Test → Authorized DAST/Network Validation → Security Gate → Production
Never blindly scan production from CI/CD.

## 🧪 Day 9 Hands-on Lab
Install on macOS if needed:
    brew install nmap
Verify:
    nmap --version
Run:
    nmap 127.0.0.1
    nmap -sV 127.0.0.1
    nmap -p 22,80,443 127.0.0.1
    nmap -p 1-1000 127.0.0.1
    nmap -sU -p 53 127.0.0.1
    nmap -sV -oN day9-scan.txt 127.0.0.1

## 🎯 Mini Challenge
1. What is host discovery?
2. What is port scanning?
3. TCP vs UDP scanning?
4. What does -sV do?
5. What does -O attempt to detect?
6. What does an open port mean?
7. Why isn't every open port a vulnerability?
8. Why should scans be scoped?
9. Why save scan results?
10. How would you investigate an unexpected SSH port?

## 🎤 Interview
**What is Nmap?** A network discovery and security auditing tool used to identify hosts, ports, services, and other network characteristics.
**Service enumeration:** Identifying the service and, when possible, its version behind an open port.
**Attack surface:** The collection of exposed points that may be reachable or exploitable by an attacker.

## 🧠 Final Tinglish Memory
> Nmap workflow: Host → Port → Service → Version → Exposure → Risk.

**Next:** Day 10 — Sniffing, Packet Capture & Wireshark.
---
# 🔥 Extra Real-World Examples & Complete Interview Coverage

## Practical Examples
### Port interpretation
If 22/tcp is open, investigate whether SSH is required, who can reach it, what version runs, and whether access is appropriately restricted.
### TCP vs UDP
A DNS service may use UDP 53. A TCP-only scan can therefore miss UDP exposure.
### Scan to risk
Nmap → open port → service → version → exposure review → vulnerability validation.
**Tinglish:** Nmap result itself final vulnerability verdict kaadu.

## 🎤 Interview Question Bank
1. What is network scanning?
2. What is host discovery?
3. What is port scanning?
4. What is service enumeration?
5. What is version detection?
6. What is OS detection?
7. What is Nmap?
8. What does -sn do?
9. What does -sV do?
10. What does -O do?
11. What does -sU do?
12. What does -p do?
13. How do you save Nmap output?
14. TCP scan vs UDP scan?
15. Open vs closed vs filtered?
16. Why can Nmap results be incomplete?
17. Why is OS detection not always accurate?
18. Why must scans be authorized?
19. What is service fingerprinting?
20. How do you interpret an unexpected open port?
21. How can scanning support vulnerability management?
22. How can network validation fit into DevSecOps?
23. Why should production scanning be controlled?
24. Nmap finds port 22 open. What next?
25. Nmap finds an unknown service. How do you investigate?
26. A scan finds many open ports. How do you prioritize investigation?

**Interview formula:** Scope → Discovery → Ports → Service/version → Exposure → Validation.
