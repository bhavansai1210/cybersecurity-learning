# Day 8 — Lab Setup, Reconnaissance & OSINT

## 🎯 Learning Goal
Build an isolated cybersecurity practice environment and understand passive/active reconnaissance and OSINT.

The course syllabus places lab setup, passive/active reconnaissance, domain information, WHOIS, DNS, subdomain enumeration, IP discovery, ASN/network ownership, technology identification, email discovery, search-engine reconnaissance, Certificate Transparency, Shodan and Censys in this stage. fileciteturn16file0

> ⚠️ Use only your own domains, lab targets, or targets where you have explicit authorization.

## 1. Cybersecurity Lab
Recommended: Kali Linux, Ubuntu, Windows VM, OWASP Juice Shop, DVWA, and Metasploitable.
**🇮🇳 Tinglish:** Real websites meeda random testing cheyyakunda isolated lab create chesukovali.

## 2. Network Modes
- NAT — useful for VM internet access
- Bridged — VM appears on the physical network
- Host-Only — useful for isolated host/VM lab communication
**🇮🇳 Tinglish:** Learning lab ki Host-Only networking useful because test traffic ni isolated environment lo keep cheyochu.

## 3. Passive vs Active Recon
**Passive:** Collect public information with minimal direct target interaction.
Examples: public records, search engines, Certificate Transparency, public DNS information.
**Active:** Directly interact with the target.
Examples: port scanning, service enumeration, direct probing.
**🇮🇳 Tinglish:** Passive = public information. Active = target tho direct interaction.

## 4. Recon Methodology
Define Scope → Collect Public Information → Identify Domains → DNS/IP Information → Identify Technologies → Map Attack Surface → Document Findings
Never skip scope.

## 5. WHOIS
WHOIS can provide registration-related information depending on the registry, privacy controls, and current service behavior.
    whois example.com
**🇮🇳 Tinglish:** Domain registration information understand cheyadaniki WHOIS useful.

## 6. DNS Reconnaissance
    dig example.com
    dig example.com A
    dig example.com MX
    dig example.com NS
**🇮🇳 Tinglish:** DNS recon tho domain-to-IP, mail servers, name servers and other DNS information understand cheyochu.

## 7. Subdomain Enumeration
Examples: www.example.com, api.example.com, mail.example.com, dev.example.com
Only enumerate authorized domains.
**🇮🇳 Tinglish:** Subdomains additional applications/services expose cheyavachu, so attack-surface mapping lo useful.

## 8. IP Address & ASN
Recon flow: Domain → IP → Network → ASN/Ownership → Related Infrastructure.
**🇮🇳 Tinglish:** ASN internet routing/network ownership context understand cheyadaniki useful.

## 9. Technology Identification
Review HTTP headers, page structure, JavaScript, TLS certificate information, error messages, and public documentation.
**🇮🇳 Tinglish:** Technologies and versions identify cheyadam attack surface understanding ki help chestundi.

## 10. Search Engine Reconnaissance
Public search engines may reveal documentation, public files, old pages, indexed subdomains, or accidentally exposed information.
Do not use discovered credentials or private data. Report exposure responsibly.

## 11. Certificate Transparency
TLS certificates are publicly logged in Certificate Transparency systems and can reveal domain names and related hostnames.

## 12. Shodan & Censys
These platforms can help researchers understand internet-exposed services and infrastructure.
Use only for authorized security research and your own assets.

## 🧪 Day 8 Safe Lab
Use a domain you own or a deliberately provided lab target.
    whois example.com
    dig example.com
    dig example.com A
    dig example.com MX
    dig example.com NS
Document domain, DNS records, name servers, mail servers, IPs, technologies, and potential attack surface.

## 🎯 Mini Challenge
1. Passive vs active reconnaissance?
2. Why define scope?
3. What is WHOIS?
4. What does DNS recon reveal?
5. What is subdomain enumeration?
6. What is ASN?
7. Why is technology identification useful?
8. What is Certificate Transparency?
9. What are Shodan/Censys used for?
10. Why must OSINT findings be handled carefully?

## 🎤 Interview
**Reconnaissance:** Collecting information about a target to understand its attack surface.
**Passive vs active:** Passive uses public information with minimal direct interaction; active directly interacts with the target.
**Scope:** Defines systems and activities authorized during security testing.

## 🧠 Final Tinglish Memory
> Recon ante first attack cheyyadam kaadu. First target ni understand cheyadam. Scope → Information → Attack Surface → Document.

**Next:** Day 9 — Network Scanning & Nmap.
---
# 🔥 Extra Real-World Examples & Complete Interview Coverage

## Practical Examples
### Passive recon
Public DNS, Certificate Transparency, public documentation and search results can help build an attack-surface map without directly probing the target.
### Active recon
An authorized Nmap scan directly interacts with the target to identify hosts, ports and services.
### Subdomain exposure
www, api, dev and old subdomains can represent different applications and should be reviewed within authorized scope.
### Recon report
Domain → IP → DNS → Subdomains → Technologies → Potential attack surface → Evidence and source.

## 🎤 Interview Question Bank
1. What is reconnaissance?
2. Why is reconnaissance important?
3. Passive vs active reconnaissance?
4. What is OSINT?
5. What is WHOIS?
6. What is DNS reconnaissance?
7. What is subdomain enumeration?
8. What is ASN?
9. What is network ownership?
10. What is technology fingerprinting?
11. What is Certificate Transparency?
12. What are Shodan and Censys?
13. What is search-engine reconnaissance?
14. Why is scope important?
15. What is an attack-surface map?
16. Why can development subdomains be security-relevant?
17. What is information disclosure?
18. How do you document recon findings?
19. Why should OSINT evidence include source and timestamp?
20. You discover an old subdomain. What do you do?
21. CT logs reveal a hostname you did not know about. What is your next step?
22. A public document exposes internal hostnames. What is the security concern?

**Interview formula:** Scope → Passive → Authorized Active → Validate → Document.
