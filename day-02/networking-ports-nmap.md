# Day 2 — Networking, Ports & Nmap

## 1. How a Request Travels

A simplified HTTPS flow:

```text
Browser
  ↓
DNS
  ↓
IP Address
  ↓
TCP connection
  ↓
TLS handshake
  ↓
HTTPS request
  ↓
Web Server
```

Security can matter at every stage.

## 2. IP Addresses

### IPv4

Example:

```text
192.168.1.10
```

IPv4 uses 32 bits.

### IPv6

Example:

```text
2001:db8::1
```

IPv6 uses 128 bits.

## 3. Private IP Ranges

Common private IPv4 ranges:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

Private addresses are intended for internal networks and are not directly routed across the public Internet.

## 4. Ports

Think of an IP address as a building address and a port as a service entry point.

```text
IP
│
├── :22    SSH
├── :80    HTTP
├── :443   HTTPS
├── :5432  PostgreSQL
└── :27017 MongoDB
```

Examples:

| Port | Service |
|---:|---|
| 22 | SSH |
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |
| 5432 | PostgreSQL |
| 3306 | MySQL |
| 27017 | MongoDB |
| 6379 | Redis |
| 9092 | Kafka |

## 5. TCP vs UDP

### TCP

TCP is connection-oriented. A simplified handshake is:

```text
Client
  │
  │ SYN
  ▼
Server
  │
  │ SYN-ACK
  ▼
Client
  │
  │ ACK
  ▼
Connection established
```

Common TCP applications include HTTPS, SSH, HTTP, and PostgreSQL.

### UDP

UDP is connectionless and has less protocol overhead.

Common examples include DNS, DHCP, streaming, and some VPN protocols.

## 6. DNS

When you enter a domain such as `google.com`, your system needs an IP address.

```text
google.com
     ↓
DNS Resolver
     ↓
IP address
```

Useful commands:

```bash
nslookup google.com
dig google.com
```

Security topics to learn later:

- DNS spoofing
- DNS poisoning
- DNSSEC
- DNS tunneling
- Domain hijacking

## 7. HTTP vs HTTPS

HTTP sends web requests without TLS protection.

HTTPS uses TLS to protect HTTP traffic in transit.

Try:

```bash
curl -I https://google.com
```

Response headers can provide information during authorized security assessments.

## 8. Nmap

Nmap (Network Mapper) is commonly used for:

- Host discovery
- Port scanning
- Service detection
- Version detection
- Network enumeration

Only scan systems you own or have explicit permission to test.

### Install on macOS

```bash
brew install nmap
nmap --version
```

### Scan localhost

```bash
nmap localhost
nmap 127.0.0.1
```

### Service/version detection

```bash
nmap -sV localhost
```

### Scan selected ports

```bash
nmap -p 22,80,443,5432,3306,27017 localhost
```

## 9. AWS Security Perspective

Example of a risky exposure:

```text
Internet
    ↓
Public IP
    ↓
EC2
    ↓
5432 PostgreSQL
```

A more controlled architecture is:

```text
Internet
   ↓
443
   ↓
Load Balancer
   ↓
Application
   ↓
Private Network
   ↓
PostgreSQL :5432
```

For AWS Security Groups, a better rule is generally to allow database access from the required application security group instead of exposing the database broadly.

## 10. Day 2 Lab

Run these commands on your own machine:

```bash
ipconfig getifaddr en0
ping -c 4 8.8.8.8
nslookup google.com
dig google.com
curl -I https://google.com
nmap localhost
nmap -sV localhost
nmap -p 22,80,443,5432,3306,27017 localhost
```

## Day 2 Mindset

Ask:

- What is exposed?
- Who can access it?
- Which ports are open?
- Which services are running?
- Should those services actually be exposed?

## Key Takeaways

- IP → where?
- Port → which service?
- TCP → reliable connection-oriented transport
- UDP → connectionless transport
- DNS → domain to IP resolution
- HTTPS → HTTP protected by TLS
- Nmap → network/service enumeration
- Firewall → controls network access
