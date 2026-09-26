# Day 1 — Cybersecurity Fundamentals

## 🎯 Learning Goal

Understand the basic security concepts that form the foundation for everything we will learn later.

---

## 1. What is Cybersecurity?

### English

Cybersecurity is the practice of protecting applications, systems, networks, identities, and data from unauthorized access, modification, destruction, or disruption.

### 🇮🇳 Tinglish

Cybersecurity ante mana **systems, applications, networks, users, and data ni unauthorized people or attackers nunchi protect cheyadam**.

Simple ga:

> "Mana system ni attacker damage cheyakunda, data steal cheyakunda, unauthorized access pondakunda protect cheyadam."

### Real-world Example

An attacker tries to log into a company's server using stolen credentials.

Security controls can detect, prevent, or limit that access.

### 🔐 Security Perspective

Security is not only about stopping hackers. It also includes:

- Preventing unauthorized access
- Protecting sensitive information
- Detecting attacks
- Responding to incidents
- Recovering systems

---

## 2. CIA Triad

CIA stands for:

- **Confidentiality**
- **Integrity**
- **Availability**

### Confidentiality

**English:** Only authorized users should be able to access information.

**Tinglish:** Confidentiality ante **data ni authorized users matrame access cheyali**.

Example: Employee salary information andariki visible ga undakudadhu.

### Integrity

**English:** Data should not be changed or modified without authorization.

**Tinglish:** Integrity ante **data ni unauthorized person modify cheyakudadhu**.

Example: Database lo patient's information attacker change chesthe integrity problem.

### Availability

**English:** Systems and data should be available when authorized users need them.

**Tinglish:** Availability ante **system required time lo users ki available ga undali**.

Example: Banking website down ayithe customers transactions cheyalearu.

### 🧠 Easy Memory Trick

```text
Confidentiality → Who can see?
Integrity       → Who can change?
Availability    → Can I access it?
```

**Tinglish:**

```text
Confidentiality → Evaru chudagalru?
Integrity       → Evaru change cheyagalru?
Availability    → System available ga unda?
```

---

## 3. Authentication vs Authorization

### Authentication

**English:** Authentication verifies **who you are**.

Examples:

- Username + password
- MFA
- SSH key
- Fingerprint
- SSO

**Tinglish:** Authentication ante:

> **"Nuvvu evaru?"**

System mana identity ni verify chestundi.

### Authorization

**English:** Authorization determines **what you are allowed to do** after authentication.

**Tinglish:** Authorization ante:

> **"Nuvvu em cheyagalavu?"**

Example:

```text
User
 ↓
Authenticated
 ↓
Role / Permissions
 ↓
Read file       ✅
Delete database ❌
```

### 🧠 Memory Trick

> Authentication = **Who are you?**

> Authorization = **What can you do?**

---

## 4. Encryption vs Hashing

### Encryption

**English:** Encryption converts readable data into ciphertext using an encryption key. The data can be decrypted using the appropriate key.

```text
Plaintext
   ↓
Encryption + Key
   ↓
Ciphertext
   ↓
Decryption + Key
   ↓
Plaintext
```

**Tinglish:** Encryption ante readable data ni **key use chesi unreadable format lo convert cheyadam**. Correct key unte malli original data ni decrypt cheyochu.

Examples:

- HTTPS/TLS
- Disk encryption
- Database encryption
- Encrypted files

### Hashing

**English:** Hashing converts data into a fixed-size value and is designed to be one-way.

```text
Password
   ↓
Password Hashing
   ↓
Stored Hash
```

**Tinglish:** Hashing ante data/password ni oka **one-way hash value** ga convert cheyadam. Normal ga hash nunchi original password ni direct ga reverse cheyalem.

Passwords should use password-hashing algorithms such as:

- Argon2
- bcrypt
- scrypt

### 🧠 Important

> Encryption = reversible with the appropriate key.

> Hashing = designed to be one-way.

---

## 5. First Networking Practical

Run these commands on your own machine:

```bash
ifconfig
ipconfig getifaddr en0
ping google.com
nslookup google.com
curl -I https://google.com
```

**Tinglish:** Ee commands tho mana machine networking basics observe cheyochu:

- Local IP
- Network connectivity
- DNS resolution
- HTTPS response
- HTTP headers

---

## 6. Security Mindset

Don't only ask:

> "Is my application working?"

Start asking:

> "Who can access it?"

> "What data can they access?"

> "What happens if credentials are stolen?"

> "What happens if an attacker gets a normal user account?"

> "Can the attacker move to a higher privilege?"

**Tinglish:** Cybersecurity mindset ante application work avtunda ani matrame kakunda:

> **"Attacker ki access vaste em cheyagaladu?"**

ani think cheyadam.

---

## 🧪 Day 1 Assignment

Run:

```bash
ifconfig
ipconfig getifaddr en0
ping -c 4 google.com
nslookup google.com
curl -I https://google.com
```

Observe:

- Your local network information
- DNS response
- Connectivity
- HTTP/HTTPS headers

---

## 🎤 Interview Questions

### Q1. What is the CIA Triad?

**Answer:** Confidentiality, Integrity, and Availability. It represents three fundamental security objectives.

**Tinglish:** Data ni unauthorized people chudakunda protect cheyadam, unauthorized changes prevent cheyadam, required time lo available ga maintain cheyadam.

### Q2. Authentication vs Authorization?

**Answer:** Authentication verifies identity; authorization determines permissions.

**Tinglish:** Authentication = "Nuvvu evaru?" Authorization = "Nuvvu em cheyagalavu?"

### Q3. Encryption vs Hashing?

**Answer:** Encryption is reversible with the appropriate key, while hashing is designed as a one-way transformation.

---

## 🧠 Day 1 Summary

```text
Cybersecurity
      ↓
Protect systems + data
      ↓
CIA Triad
      ↓
Authentication
      ↓
Authorization
      ↓
Encryption
      ↓
Hashing
      ↓
Networking Fundamentals
```

**Next:** Day 2 — Networking, Ports & Nmap.

---
# 🔥 Extra Real-World Examples & Complete Interview Coverage

## Practical Examples
**Confidentiality:** Hospital patient data should be accessible only to authorized people. If everyone can view it, confidentiality is broken.
**Integrity:** If an attacker changes a bank account number before payment, integrity is affected.
**Availability:** If a banking website is unavailable to legitimate users, availability is affected.
**Authentication + Authorization:** Employee logs in with password + MFA = authentication. Developer role allows reading code but not deleting production data = authorization.
**Encryption vs Hashing:** TLS protects data in transit using encryption. Password storage should use dedicated password hashing such as Argon2id, bcrypt, or scrypt.

## 🎤 Interview Question Bank
1. What is cybersecurity?
2. What is the CIA Triad?
3. Explain Confidentiality with an example.
4. Explain Integrity with an example.
5. Explain Availability with an example.
6. What is authentication?
7. What is authorization?
8. Authentication vs authorization?
9. What is MFA?
10. What is least privilege?
11. What is encryption?
12. What is hashing?
13. Encryption vs hashing?
14. Why should plaintext passwords not be stored?
15. What is an attack surface?
16. Why is networking knowledge important for cybersecurity?
17. A user can log in but cannot delete a database. Which security concept controls this?
18. An attacker modifies a transaction. Which CIA property is affected?
19. A website is unavailable. Which CIA property is affected?
20. A database password is leaked. What should a security analyst investigate next?

**Interview formula:** Definition → Real example → Security impact.
