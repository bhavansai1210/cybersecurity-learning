# Day 2 — Networking, Ports & Nmap

## 🎯 Learning Goal

Understand how devices communicate and how security professionals identify exposed services during authorized security testing.

---

## 1. How a Request Travels

Suppose you open:

```text
https://example.com
```

A simplified flow is:

```text
Browser
  ↓
DNS
  ↓
IP Address
  ↓
TCP Connection
  ↓
TLS Handshake
  ↓
HTTPS Request
  ↓
Web Server
```

**Tinglish:** Manam browser lo website open chesthe direct ga website ki velladu.

1. Domain ki IP address find chestundi.
2. Server tho network connection establish chestundi.
3. HTTPS ayithe TLS security establish chestundi.
4. Request server ki pampistundi.
5. Server response istundi.

Cybersecurity lo ee stages anni important.

---

## 2. IP Addresses

### IPv4

Example:

```text
192.168.1.10
```

IPv4 uses 32 bits.

**Tinglish:** IP address ante network lo oka device ki **address** laga think cheyochu.

> House ki address untundi. Network lo device ki IP address untundi.

---

## 3. Private IP Addresses

Common private IPv4 ranges:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

**Tinglish:** Private IPs mostly internal networks lo use chestaru.

Example:

```text
Laptop
192.168.1.10

Router
192.168.1.1
```

Internet lo direct ga ee private IP addresses route avvavu.

---

## 4. Ports

Think of:

```text
IP address = Building address
Port = Specific service/door
```

Example:

```text
192.168.1.10:443
```

Means:

> Connect to port 443 on 192.168.1.10.

### Common Ports

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

**Tinglish:** Oka server lo multiple services run avvachu.

```text
Server
│
├── 22   → SSH
├── 80   → HTTP
├── 443  → HTTPS
└── 5432 → PostgreSQL
```

Port ante **ee service tho communicate cheyalo identify cheyadaniki** use avtundi.

---

## 5. TCP vs UDP

### TCP

TCP is connection-oriented.

Simplified handshake:

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

**Tinglish:** TCP lo communication start cheyyadaniki connection establish chestaru.

Simple ga:

> "Nenu connect avvadaniki ready."

> "Server: okay, nenu kuda ready."

> "Client: okay, start cheddam."

This is called the **three-way handshake**.

### UDP

UDP is connectionless and has less protocol overhead.

Common examples:

- DNS
- DHCP
- Streaming
- Some VPN protocols

**Tinglish:** UDP lo TCP laga same handshake undadu. Usually speed and low overhead important ayinappudu UDP useful.

---

## 6. DNS

Suppose you type:

```text
google.com
```

Your machine needs an IP address.

```text
google.com
     ↓
DNS Resolver
     ↓
IP Address
```

Run:

```bash
nslookup google.com
dig google.com
```

**Tinglish:** DNS ni simple ga:

> **"Internet phonebook"**

ani remember chesko.

Manam domain name gurthupettukuntam:

```text
google.com
```

Computer communication kosam IP address use chestundi. DNS domain ni IP ki resolve chestundi.

---

## 7. HTTP vs HTTPS

HTTP:

```text
Client
  ↓
HTTP
  ↓
Server
```

HTTPS:

```text
Client
  ↓
TLS
  ↓
Encrypted HTTP
  ↓
Server
```

Run:

```bash
curl -I https://google.com
```

**Tinglish:** HTTP traffic ki TLS protection undadu. HTTPS ante:

> **HTTP + TLS**

TLS communication ni transit lo protect cheyadaniki use avtundi.

---

## 8. Nmap

Nmap means **Network Mapper**.

It is commonly used for:

- Host discovery
- Port scanning
- Service detection
- Version detection
- Network enumeration

**Tinglish:** Nmap ni cybersecurity lo important enumeration tool laga use chestam.

Example:

> Oka authorized server lo em ports open unnayi?

> Aa ports venaka em services run avtunnayi?

ani identify cheyadaniki Nmap help chestundi.

⚠️ Only scan systems you own or have explicit permission to test.

---

## 9. Install Nmap on macOS

```bash
brew install nmap
nmap --version
```

---

## 10. Scan Your Own Machine

Safest starting point:

```bash
nmap localhost
```

or:

```bash
nmap 127.0.0.1
```

**Tinglish:** `localhost` ante **mana own machine**. So first Nmap practice localhost meeda cheyadam safe and useful.

---

## 11. Service / Version Detection

Run:

```bash
nmap -sV localhost
```

`-sV` attempts service/version detection.

Example output:

```text
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH ...
```

**Tinglish:** Port open undi ani teliste saripodu.

Security assessment lo:

> "Ee port venaka exact ga em service/version run avtundi?"

ani kuda telusukovali. `-sV` daniki help chestundi.

---

## 12. Scan Specific Ports

```bash
nmap -p 22,80,443,5432,3306,27017 localhost
```

**Tinglish:** Manaki interesting unna specific ports matrame scan cheyochu.

---

## 13. Security Mindset

When you see a server, don't only ask:

> "Is it working?"

Ask:

```text
What ports are open?
        ↓
What services are running?
        ↓
What versions are running?
        ↓
Who can reach them?
        ↓
Should they be exposed?
        ↓
Are they vulnerable?
```

**Tinglish:** Cybersecurity mindset ante:

> **"Em expose ayindi? Evaru access cheyagalru? Enduku expose chesam? Vulnerability unda?"**

ani continuously question cheyadam.

---

## 🧪 Day 2 Lab

Run only on your own machine:

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

---

## 🎤 Interview Questions

### Q1. What is an IP address?

**English:** An IP address identifies a device/interface on a network.

**Tinglish:** Network lo device ni identify cheyadaniki IP address use chestam.

### Q2. What is a port?

**English:** A port identifies a network service endpoint on a host.

**Tinglish:** Oka server lo particular service ni identify/access cheyadaniki port use chestam.

### Q3. TCP vs UDP?

**English:** TCP is connection-oriented; UDP is connectionless and has lower protocol overhead.

**Tinglish:** TCP connection establish chesi reliable communication provide chestundi. UDP connectionless and comparatively lightweight.

### Q4. What is DNS?

**English:** DNS resolves domain names to IP addresses and supports other DNS records.

**Tinglish:** DNS domain name ni IP address ki resolve chestundi.

### Q5. What is Nmap?

**English:** Nmap is a network discovery and security auditing tool used for authorized enumeration.

**Tinglish:** Authorized systems lo hosts, ports, services, and versions identify cheyadaniki Nmap use chestam.

---

## 🧠 Day 2 Summary

```text
IP       → Where is the host?
Port     → Which service?
TCP      → Connection-oriented
UDP      → Connectionless
DNS      → Domain resolution
HTTPS    → HTTP protected by TLS
Nmap     → Enumeration
Firewall → Controls network access
```

### 🇮🇳 Tinglish Memory

```text
IP       → Ekkada?
Port     → Ye service?
TCP      → Reliable connection
UDP      → Lightweight connectionless
DNS      → Domain → IP
HTTPS    → Secure HTTP using TLS
Nmap     → Em expose ayindo identify cheyadaniki
Firewall → Evarini allow/block cheyalo control
```

**Next:** Day 3 — Linux Security.
