# Cybersecurity Roadmap

## Phase 1 — Security Fundamentals

- CIA Triad
- Authentication vs Authorization
- Encryption and hashing
- TCP/IP, DNS, HTTP/HTTPS
- Firewalls, VPNs, proxies
- Linux security basics
- Windows security basics

## Phase 2 — Networking

- OSI and TCP/IP models
- Ports and protocols
- Subnets
- Routing
- NAT
- DNS
- HTTP/HTTPS
- TLS
- Wireshark

## Phase 3 — Linux & Security Tools

- Linux permissions
- SSH
- Processes and services
- Logs
- `nmap`
- Wireshark
- Burp Suite
- `curl`
- `netcat`
- OpenSSL

## Phase 4 — Web Security

Study the OWASP Top 10, including:

- Broken access control
- Cryptographic failures
- Injection
- Insecure design
- Security misconfiguration
- Vulnerable and outdated components
- Identification and authentication failures
- Software and data integrity failures
- Security logging and monitoring failures
- Server-side request forgery

## Phase 5 — Cloud Security

Focus on AWS security:

- IAM
- Least privilege
- S3 security
- VPC security
- Security Groups and NACLs
- CloudTrail
- GuardDuty
- AWS WAF
- Secrets Manager / Parameter Store
- KMS
- AWS Config
- Security Hub

## Phase 6 — DevSecOps

Target pipeline:

```text
Developer
   ↓
Git
   ↓
SAST
   ↓
Dependency Scan
   ↓
Secret Scan
   ↓
Container Scan
   ↓
IaC Scan
   ↓
Build
   ↓
Deploy
   ↓
DAST
   ↓
Cloud / Kubernetes
   ↓
Monitoring + SIEM
```

Tools to learn:

- Trivy
- Semgrep
- SonarQube
- Gitleaks
- Checkov
- OWASP ZAP
- Falco
- GitLab Security
- GitHub security features

## Career Direction

A practical path from DevOps is:

```text
DevOps Engineer
      ↓
DevSecOps
      ↓
Cloud Security / Cloud DevSecOps
      ↓
Senior DevSecOps / Cloud Security Engineer
```
