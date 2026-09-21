# Day 1 — Cybersecurity Fundamentals

## 1. What is Cybersecurity?

Cybersecurity means protecting applications, servers, networks, databases, cloud infrastructure, identities, and data from unauthorized access, modification, destruction, or disruption.

## 2. CIA Triad

| Principle | Meaning | Example |
|---|---|---|
| Confidentiality | Only authorized people can access data | IAM permissions |
| Integrity | Data should not be modified improperly | Database access controls |
| Availability | Systems should remain accessible | Load balancing and backups |

Example:

```text
AWS S3 Bucket
      │
      ├── Confidentiality → Who can read?
      ├── Integrity       → Who can modify?
      └── Availability    → Can users access it?
```

## 3. Authentication vs Authorization

### Authentication

Authentication answers:

> Who are you?

Examples:

- Password
- MFA
- SSH key
- OAuth
- SSO

### Authorization

Authorization answers:

> What are you allowed to do?

Example:

```text
User
  ↓
Authenticated
  ↓
IAM Role
  ↓
S3:GetObject ✅
S3:DeleteBucket ❌
```

Memory trick:

> Authentication → Who are you?
>
> Authorization → What can you do?

## 4. Encryption vs Hashing

### Encryption

Encryption is reversible with the appropriate key.

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

Common uses:

- HTTPS/TLS
- Database encryption
- S3 encryption
- Disk encryption

### Hashing

Hashing is designed to be one-way.

```text
Password
   ↓
Password Hashing
   ↓
Stored Hash
```

Passwords should be stored using a password hashing algorithm such as Argon2, bcrypt, or scrypt rather than plaintext.

## 5. First Networking Practical

Run:

```bash
ifconfig
ipconfig getifaddr en0
ping google.com
nslookup google.com
curl -I https://google.com
```

These commands expose concepts including local addressing, DNS, network reachability, HTTPS, and HTTP response headers.

## Key Takeaways

- CIA = Confidentiality, Integrity, Availability
- Authentication = identity
- Authorization = permissions
- Encryption protects data with keys
- Hashing is designed as a one-way transformation
- Networking fundamentals are essential for cybersecurity
