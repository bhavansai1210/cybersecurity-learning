# Day 10 — Sniffing, Packet Analysis & Wireshark

## 🎯 Learning Goal
Understand network packet capture and analyze TCP, UDP, DNS, HTTP, and TLS traffic using Wireshark in an authorized lab.

The syllabus includes network sniffing concepts, packet capture, promiscuous mode, Wireshark, and TCP/UDP packet analysis. fileciteturn16file0

> ⚠️ Capture traffic only on networks and devices you own or are explicitly authorized to monitor. Do not capture other people's private traffic.

## 1. What is Packet Sniffing?
Packet sniffing means observing network packets as they move through a network interface.
**🇮🇳 Tinglish:** Network lo data packets ga travel avtundi. Capture chesi source, destination, protocol, port, and visible information analyze cheyachu.

## 2. Why Packet Analysis Matters
Security analysts use packet analysis to investigate suspicious connections, DNS activity, malware communication, scanning, protocol problems, unusual outbound traffic, and incident timelines.

## 3. Promiscuous Mode
Promiscuous mode can allow an interface to receive more frames from the local network segment, depending on the network and capture environment.
**🇮🇳 Tinglish:** Interface ki available ayye broader network frames ni capture cheyadaniki mode laga think cheyyachu. It does not magically expose all internet traffic.

## 4. Wireshark Workflow
Select Interface → Start Capture → Generate Test Traffic → Stop → Apply Filters → Analyze

## 5. Safe Capture Lab
Use your own machine.
Generate traffic:
    ping example.com
    curl -I https://example.com
Capture for a short period and stop.

## 6. Packet Fields
Common fields:
- Source
- Destination
- Protocol
- Source port
- Destination port
- Length
- Flags
- Sequence information
**🇮🇳 Tinglish:** Source = evaru pampincharu? Destination = ekkadiki? Protocol = TCP/UDP/DNS/HTTP? Port = ye service?

## 7. TCP Analysis
Common TCP 3-way handshake:
    Client → SYN → Server
    Client ← SYN/ACK ← Server
    Client → ACK → Server
**🇮🇳 Tinglish:** SYN → SYN/ACK → ACK.

## 8. TCP Flags
Common flags: SYN, ACK, FIN, RST, PSH.
Repeated unusual RST traffic can be a clue, but a single flag is not proof of an attack.

## 9. UDP Analysis
UDP is connectionless and is commonly used by DNS and real-time applications.
**🇮🇳 Tinglish:** UDP lo TCP laga handshake undadu.

## 10. DNS Analysis
Wireshark filter:
    dns
Inspect query name, query type, response, and response IP.
**🇮🇳 Tinglish:** System ye domain ni resolve cheyadaniki try chestundo identify cheyachu.

## 11. HTTP Analysis
Filter:
    http
HTTP can expose application data in plaintext depending on the traffic.
**🇮🇳 Tinglish:** HTTP encrypted kaadu; lab traffic capture chesthe request details visible ga undochu.

## 12. HTTPS / TLS Analysis
Filter:
    tls
Packet capture can still reveal metadata such as source/destination IPs, ports, packet sizes, timing, and TLS handshake information. Correctly configured TLS protects application payload.
**🇮🇳 Tinglish:** HTTPS use chesthe traffic undani telustundi, but application data generally plaintext ga visible undadu.

## 13. Useful Filters
    ip.addr == 192.168.1.10
    tcp
    udp
    dns
    http
    tls
    tcp.port == 443
    udp.port == 53
    icmp
Replace the example IP with your own lab value.

## 14. Follow TCP Stream
Wireshark can reconstruct a TCP conversation for analysis. Use Right-click packet → Follow → TCP Stream.
**🇮🇳 Tinglish:** Oka conversation ni complete flow laga chudachu. Use only on authorized traffic.

## 15. Suspicious Behavior
Potential clues include:
- One source contacting many destination ports
- Unexpected DNS domains
- Unexpected external connections
- Unusual protocols or ports
**🇮🇳 Tinglish:** Goal is normal behavior ni understand chesi unusual behavior ni investigate cheyadam.

## 16. Wireshark and SOC
Alert → Identify Host → Check Logs → PCAP → Analyze DNS/Connections → Identify IOC → Build Timeline → Incident Response
**🇮🇳 Tinglish:** SIEM alert vachinappudu PCAP available unte network evidence tho alert ni validate cheyachu.

## 17. DevSecOps Connection
CI/CD → Test Deployment → Authorized Traffic Capture → Analyze TLS/DNS/HTTP → Validate Security Controls
This can help verify encrypted transport and expected network behavior in test environments.

## 🧪 Day 10 Hands-on Lab
1. Open Wireshark and select your own active interface.
2. Start a short capture.
3. Run:
    ping example.com
    curl -I https://example.com
4. Apply filters: dns, icmp, tcp, tls, tcp.port == 443.
5. Find your source IP, destination IP, DNS query, TCP handshake, TLS traffic, and destination port.
6. Document: Protocol, Source, Destination, Port, Observation, Security relevance.

## 🎯 Mini Challenge
1. What is packet sniffing?
2. What is Wireshark?
3. What is promiscuous mode?
4. Explain TCP 3-way handshake.
5. TCP vs UDP?
6. What can DNS packets reveal?
7. HTTP vs HTTPS from packet-analysis perspective?
8. What does TLS protect?
9. What is a Wireshark display filter?
10. How can packet analysis help a SOC analyst?

## 🎤 Interview
**What is Wireshark?** A network protocol analyzer used to capture and inspect network traffic.
**What is packet sniffing?** Observing and analyzing network packets.
**TCP 3-way handshake?** SYN → SYN/ACK → ACK.
**Why is HTTPS safer than HTTP?** HTTPS uses TLS to protect HTTP application data in transit and authenticate the server through certificate-based mechanisms.
**How can Wireshark help incident response?** It provides packet-level evidence for connections, DNS activity, protocols, timing, and other network behavior.

## 🧠 Final Tinglish Memory
> Wireshark ante packets ni just chudadam kaadu. Source, destination, protocol, port, timing, behavior anni combine chesi “Ee traffic normal aa? Suspicious aa? Enduku?” ani analyze cheyadam.

**Next:** Day 11 — Web Security & OWASP Fundamentals.
---
# 🔥 Extra Real-World Examples & Complete Interview Coverage

## Practical Examples
### TCP handshake
Client → SYN → Server → SYN/ACK → Client → ACK.
**Tinglish:** Ee sequence TCP connection establish avvadaniki common starting flow.
### DNS investigation
Host → DNS query → DNS response → connection to returned IP. SOC analysts can correlate DNS and network events.
### HTTP vs HTTPS
HTTP lab traffic may expose application details. Correctly configured HTTPS protects application payload with TLS, while metadata such as IPs and timing may still be observable.
### SOC investigation
Alert → Host → Endpoint logs → DNS → PCAP → IOC → Timeline → Incident Response.

## 🎤 Interview Question Bank
1. What is packet sniffing?
2. What is packet capture?
3. What is Wireshark?
4. What is promiscuous mode?
5. Does promiscuous mode expose all internet traffic?
6. What is a packet?
7. What are source and destination?
8. What is a protocol?
9. Explain TCP three-way handshake.
10. What are SYN, ACK, FIN and RST?
11. TCP vs UDP?
12. How do you analyze DNS traffic?
13. What can HTTP reveal?
14. What does TLS protect?
15. What metadata may remain visible with HTTPS?
16. What is a Wireshark display filter?
17. What is Follow TCP Stream?
18. How can packet analysis detect scanning?
19. How can packet analysis support malware investigation?
20. How can PCAP support incident response?
21. What is an IOC?
22. Why is a timeline important?
23. Why should captures be authorized?
24. One host contacts many ports. What might this indicate?
25. A workstation queries an unusual domain and immediately connects to its IP. What would you investigate?
26. You see repeated RST packets. Is that automatically malicious?
27. HTTPS traffic is visible in Wireshark. Does that mean the payload is readable?
28. A SIEM alert says a host contacted a suspicious IP. How could PCAP help validate it?

**Interview formula:** Capture → Filter → Protocol → Correlate → Investigate → Document.
