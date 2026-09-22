# Day 5 — Cryptography Fundamentals

## 🎯 Learning Goal

Understand the core cryptography concepts used in cybersecurity:

- Plaintext and ciphertext
- Encryption and decryption
- Symmetric encryption
- Asymmetric encryption
- Hashing
- Password hashing
- Salting
- Digital signatures
- Public Key Infrastructure (PKI)
- Digital certificates
- TLS
- Common cryptographic mistakes

> ⚠️ Cryptography is about protecting information. Practice only with data and systems you own or are authorized to test.

---

## 1. What is Cryptography?

### 🇬🇧 English

Cryptography is the science of protecting information by transforming it so that only authorized parties can access, verify, or use it.

Cryptography provides security properties such as:

- Confidentiality
- Integrity
- Authentication
- Non-repudiation

### 🇮🇳 Tinglish

Cryptography ante **data ni secure cheyadaniki mathematical techniques and algorithms use cheyadam**.

Simple ga:

> "Attacker data chusina kuda useful information ardham kakunda, or data change ayithe detect cheyagalige laga protect cheyadam."

---

# 2. Plaintext and Ciphertext

### Plaintext

Original readable data.

Example:

~~~text
Hello Bhavan
~~~

### Ciphertext

Encrypted, unreadable-looking output.

~~~text
8fA2...xK91
~~~

### Flow

~~~text
Plaintext
    ↓
Encryption + Key
    ↓
Ciphertext
    ↓
Decryption + Key
    ↓
Plaintext
~~~

### 🇮🇳 Tinglish

Plaintext ante original readable data.

Ciphertext ante encryption ayyaka vachina protected data.

> Plaintext → lock cheyyadam → Ciphertext → correct key tho unlock → Plaintext

---

# 3. Keys

A cryptographic key is information used by a cryptographic algorithm to perform encryption, decryption, signing, or verification.

### 🇮🇳 Tinglish

Key ni simple ga **digital secret/control value** laga imagine cheyyi.

Encryption algorithm matrame secret ga undalsina avasaram ledu.

Good cryptographic design generally assumes:

> **Algorithm public ga telisina kuda secret key secure ga unte security maintain avvali.**

This is related to **Kerckhoffs's principle**.

---

# 4. Symmetric Encryption

Symmetric encryption uses the **same secret key** for encryption and decryption.

~~~text
                Same Secret Key
                      │
Plaintext ──→ Encryption ──→ Ciphertext
                                │
                                ↓
                           Decryption
                                │
                                ↓
                             Plaintext
~~~

Common algorithm:

- AES

### Example

~~~text
Message + Secret Key
        ↓
       AES
        ↓
   Ciphertext
~~~

### 🇮🇳 Tinglish

Symmetric encryption lo **same key** encryption and decryption rendu kosam use chestam.

Example:

> Nenu oka secret key tho file encrypt chesa. Same secret key tho authorized person decrypt cheyali.

### Main Challenge

**Key distribution**

Question:

> Secret key ni receiver ki secure ga ela provide cheyyali?

Idi symmetric cryptography lo important challenge.

---

# 5. Asymmetric Encryption

Asymmetric cryptography uses a **key pair**:

- Public key
- Private key

~~~text
Public Key
   ↓
Can be shared

Private Key
   ↓
Must be protected
~~~

### 🇮🇳 Tinglish

Asymmetric cryptography lo two related keys untayi.

> **Public key** → share cheyochu.

> **Private key** → secret ga protect cheyali.

Private key leak ayithe serious security problem.

---

# 6. Encryption with Public and Private Keys

A simplified confidentiality example:

~~~text
Sender
   ↓
Encrypt using Receiver's Public Key
   ↓
Ciphertext
   ↓
Receiver
   ↓
Decrypt using Receiver's Private Key
   ↓
Plaintext
~~~

### 🇮🇳 Tinglish

Nuvvu receiver ki secret message pampali anuko.

Receiver public key ni use chesi encrypt cheyochu.

Receiver tana private key tho decrypt chestadu.

> Public key share cheyochu; private key secret ga undali.

---

# 7. Digital Signatures

Digital signatures are primarily used to provide:

- Integrity
- Authentication
- Evidence that a particular private key was used to sign

Simplified flow:

~~~text
Message
   ↓
Hash
   ↓
Sign with Private Key
   ↓
Digital Signature
~~~

Verification:

~~~text
Message + Signature
        ↓
Verify using Public Key
        ↓
Valid / Invalid
~~~

### 🇮🇳 Tinglish

Digital signature ni physical signature laga only imagine cheyyakudadhu.

Security perspective lo:

> "Ee data change ayinda?"

> "Valid private key tho sign chesara?"

ani verify cheyadaniki help chestundi.

---

# 8. Hashing

Hashing is a one-way transformation that produces a fixed-length digest for a given input.

Example:

~~~text
Input
  ↓
Hash Function
  ↓
Digest
~~~

Common cryptographic hash functions:

- SHA-256
- SHA-512

### 🇮🇳 Tinglish

Hashing ante data ni fixed-length output ga convert cheyadam.

Important:

> **Hashing encryption kaadu.**

Encryption lo appropriate key tho decrypt cheyochu.

Hashing designed to be one-way.

---

# 9. Hash Example

On macOS/Linux:

~~~bash
printf "hello" | shasum -a 256
~~~

On Windows PowerShell:

~~~powershell
"hello" | ForEach-Object { [Convert]::ToHexString(( [System.Security.Cryptography.SHA256]::HashData([System.Text.Encoding]::UTF8.GetBytes($_)))) }
~~~

You should get a deterministic SHA-256 digest for the same exact input.

### 🇮🇳 Tinglish

Same input + same hash algorithm → same digest.

But even a small input change can produce a very different digest.

For example:

~~~text
hello
Hello
~~~

case change valla hash kuda completely different ga untundi.

---

# 10. Password Hashing

Passwords should not be stored as plaintext.

Bad:

~~~text
username: bhavan
password: MyPassword123
~~~

Better:

~~~text
username: bhavan
password_hash: <password hash>
~~~

For password storage, use dedicated password-hashing algorithms such as:

- Argon2id
- bcrypt
- scrypt

### 🇮🇳 Tinglish

Application database leak ayina situation imagine cheyyi.

Plaintext passwords unte attacker direct ga use cheyagaladu.

Password hashing use chesthe attacker ki stored password representation matrame dorukutundi.

But:

> **Weak password hashing or weak passwords can still be attacked offline.**

---

# 11. Salt

A salt is a unique random value added to a password before password hashing.

Simplified:

~~~text
Password + Unique Salt
          ↓
   Password Hashing
          ↓
     Stored Result
~~~

### 🇮🇳 Tinglish

Same password use chesina two users ki same stored hash ravakunda salt help chestundi.

Example:

~~~text
User A
Password + Salt A
      ↓
    Hash A

User B
Password + Salt B
      ↓
    Hash B
~~~

Salt:

- Should be unique
- Does not need to be secret
- Should be stored with the password hash

---

# 12. Hashing vs Encryption

| Feature | Hashing | Encryption |
|---|---|---|
| Main purpose | Integrity / fingerprints / password storage | Confidentiality |
| Reversible? | Designed to be one-way | Yes, with appropriate key |
| Key required? | Cryptographic hash normally no | Yes |
| Example | SHA-256 | AES |
| Password storage | Dedicated password hash | Not appropriate by itself |

### 🇮🇳 Tinglish

Easy memory:

> **Encryption → Hide**

> **Hashing → Fingerprint**

---

# 13. Symmetric vs Asymmetric

| Feature | Symmetric | Asymmetric |
|---|---|---|
| Keys | One shared secret | Public + private |
| Speed | Generally faster | Generally slower |
| Main challenge | Secure key distribution | Private key protection |
| Example | AES | RSA / ECC |
| Common use | Bulk data encryption | Key exchange, signatures, identity |

### 🇮🇳 Tinglish

Simple ga:

> Symmetric = **One secret key**

> Asymmetric = **Public + Private key pair**

Modern protocols often combine both approaches.

---

# 14. Hybrid Cryptography

Real-world secure protocols commonly combine symmetric and asymmetric cryptography.

Simplified idea:

~~~text
Asymmetric Cryptography
        ↓
Securely establish / protect a session key
        ↓
Symmetric Cryptography
        ↓
Encrypt large amounts of data efficiently
~~~

### 🇮🇳 Tinglish

Asymmetric cryptography generally slower.

Symmetric cryptography generally faster.

So real-world systems:

> **Asymmetric → key establishment**

> **Symmetric → bulk data encryption**

laga combine cheyochu.

---

# 15. TLS and HTTPS

HTTPS is HTTP protected by TLS.

Simplified:

~~~text
Browser
   ↓
TLS Handshake
   ↓
Secure Session
   ↓
HTTPS Data
   ↓
Server
~~~

TLS uses cryptographic mechanisms for authentication, key establishment, and protecting application data in transit.

### 🇮🇳 Tinglish

Manam website open chesthe:

~~~text
https://example.com
~~~

HTTPS lo TLS use avtundi.

TLS server identity ni certificate-based mechanisms tho verify cheyadaniki and secure session establish cheyadaniki cryptography use chestundi.

---

# 16. Digital Certificates

A digital certificate binds an identity such as a domain name to a public key and is signed by a certificate authority (CA).

Typical certificate information can include:

- Domain names
- Public key
- Issuer
- Validity period
- Signature
- Certificate details

### 🇮🇳 Tinglish

Certificate ni simple ga:

> **"Ee public key ee identity/domain ki belong avtundi"**

ani prove cheyadaniki use ayye signed document laga think cheyyi.

Browser certificate ni verify chestundi.

---

# 17. Certificate Authorities — CA

A Certificate Authority issues and signs certificates.

Simplified trust chain:

~~~text
Root CA
   ↓
Intermediate CA
   ↓
Server Certificate
   ↓
Website Identity
~~~

### 🇮🇳 Tinglish

Browser every website owner ni personally telusukodu.

Trusted Certificate Authorities meeda trust model build chestundi.

Certificate valid and trusted chain lo unte browser secure connection establish cheyadaniki proceed chestundi.

---

# 18. Public Key Infrastructure — PKI

PKI is a system of technologies, policies, certificates, keys, and trust relationships used to manage public-key cryptography.

PKI commonly involves:

- Public/private keys
- Certificates
- Certificate Authorities
- Certificate validation
- Trust chains
- Revocation mechanisms

### 🇮🇳 Tinglish

PKI ante just certificate okkate kaadu.

> **Keys + Certificates + CA + Trust + Validation**

anni kalisi public-key security ecosystem create chestayi.

---

# 19. Randomness Matters

Cryptography requires high-quality randomness for things such as:

- Keys
- Nonces
- Salts
- Tokens

Weak randomness can weaken otherwise strong cryptographic algorithms.

### 🇮🇳 Tinglish

Strong algorithm use chesina random values predictable ga unte security break avvachu.

So:

> **Cryptography lo randomness chala important.**

---

# 20. Nonce

A nonce is a value intended to be used in a cryptographic protocol according to specific uniqueness requirements.

The exact requirements depend on the algorithm/protocol.

### 🇮🇳 Tinglish

Nonce ni simple ga:

> **"Ee cryptographic operation/context ki unique value"**

laga think cheyochu.

Nonce requirements algorithm-specific.

Wrong nonce reuse some cryptographic schemes lo serious vulnerability create cheyachu.

---

# 21. Common Cryptography Mistakes

### ❌ Rolling your own encryption

Don't invent your own cryptographic algorithm.

### ❌ Hardcoding secrets

Don't hardcode encryption keys or private keys into source code.

### ❌ Using obsolete algorithms

Avoid outdated or broken algorithms for new systems.

### ❌ Storing plaintext passwords

Use dedicated password-hashing algorithms.

### ❌ Reusing sensitive keys everywhere

Keys should have appropriate scope, lifecycle, and protection.

### ❌ Ignoring certificate validation

Certificate validation is an important part of TLS security.

### 🇮🇳 Tinglish

Cryptography lo biggest lesson:

> **"Strong algorithm choose cheyyadam matrame saripodu. Correct implementation and key management equally important."**

---

# 22. Key Management

Cryptographic security often depends more on key management than simply selecting an algorithm.

Important topics:

- Key generation
- Key storage
- Key access control
- Key rotation
- Key backup
- Key revocation
- Key destruction

### 🇮🇳 Tinglish

Encryption key attacker ki dorikithe:

> Strong AES use chesina kuda problem.

Kabatti:

> **Key ni ekkada store chestunnam? Evaru access cheyagalru? Eppudu rotate cheyali?**

ani think cheyali.

---

# 23. Practical Hash Lab

### macOS / Linux

Create a test file:

~~~bash
echo "Cybersecurity Day 5" > crypto-test.txt
~~~

Calculate SHA-256:

~~~bash
shasum -a 256 crypto-test.txt
~~~

Modify the file:

~~~bash
echo "Modified" >> crypto-test.txt
~~~

Calculate the hash again:

~~~bash
shasum -a 256 crypto-test.txt
~~~

### 🇮🇳 Tinglish

First hash note chesko.

File lo small change chesaka second hash calculate cheyyi.

Compare:

> **Hash change ayinda?**

Yes.

Idi integrity checking concept ni understand cheyadaniki useful.

---

# 24. Practical OpenSSL Lab

Check OpenSSL:

~~~bash
openssl version
~~~

Generate a SHA-256 digest:

~~~bash
printf "Cybersecurity" | openssl dgst -sha256
~~~

Generate a random value for learning:

~~~bash
openssl rand -hex 16
~~~

> These commands are for learning. Don't use casually generated terminal secrets as production key-management practice.

---

# 25. Practical Certificate Inspection

Inspect a public HTTPS certificate:

~~~bash
openssl s_client -connect example.com:443 -servername example.com
~~~

Then exit with:

~~~text
QUIT
~~~

You can observe certificate and TLS information.

### 🇮🇳 Tinglish

Ee lab tho:

- TLS connection
- Certificate
- Server identity
- Public key information
- Certificate chain

lanti concepts ni observe cheyochu.

---

# 🎯 Day 5 Mini Challenge

Answer these without looking at the notes:

1. What is cryptography?
2. What is the difference between plaintext and ciphertext?
3. Symmetric encryption lo enni secret keys?
4. Asymmetric cryptography lo key pair enti?
5. What is hashing?
6. Why should passwords use Argon2id/bcrypt/scrypt instead of plaintext?
7. What is a salt?
8. Encryption vs hashing difference enti?
9. What is a digital signature?
10. What is a digital certificate?
11. What is a Certificate Authority?
12. What is PKI?
13. Why is key management important?
14. Why does HTTPS use TLS?

---

# 🎤 Interview Questions

### Q1. What is encryption?

**English:** Encryption transforms plaintext into ciphertext using a cryptographic algorithm and key so that authorized parties can recover the protected data.

**Tinglish:** Readable data ni key use chesi protected ciphertext ga convert cheyadam encryption.

### Q2. Symmetric vs asymmetric encryption?

**English:** Symmetric encryption uses a shared secret key, while asymmetric cryptography uses a public/private key pair.

**Tinglish:** Symmetric = one shared secret key. Asymmetric = public key + private key.

### Q3. What is hashing?

**English:** Hashing is a one-way transformation that produces a fixed-length digest from input data.

**Tinglish:** Data ni one-way fixed-length digest ga convert cheyadam hashing.

### Q4. Why are passwords hashed?

**English:** Passwords are hashed so the application does not need to store the original plaintext password.

**Tinglish:** Database leak ayina direct plaintext passwords attacker ki dorakakunda password-hashing use chestam.

### Q5. What is a salt?

**English:** A salt is a unique random value used with password hashing to make precomputed attacks and identical-password hash matching more difficult.

**Tinglish:** Same password ki different users different stored hashes ravadaniki unique salt use chestam.

### Q6. What is a digital signature?

**English:** A digital signature provides a mechanism to verify integrity and that a signature was created using the corresponding private key.

**Tinglish:** Data change ayinda and corresponding private key tho sign chesara ani verify cheyadaniki digital signature use chestam.

### Q7. What is PKI?

**English:** PKI is the framework of keys, certificates, certificate authorities, trust, and validation used to support public-key cryptography.

**Tinglish:** Public/private keys, certificates, CA, trust, validation anni kalisi PKI ecosystem create chestayi.

---

# 🧠 Day 5 Summary

~~~text
Cryptography
     ↓
Plaintext / Ciphertext
     ↓
Keys
     ↓
Symmetric Encryption
     ↓
Asymmetric Cryptography
     ↓
Hashing
     ↓
Password Hashing + Salt
     ↓
Digital Signatures
     ↓
Certificates
     ↓
CA / PKI
     ↓
TLS / HTTPS
     ↓
Key Management
~~~

## 🇮🇳 Final Tinglish Memory

> **Encryption = Data ni hide cheyadam.**

> **Hashing = Data ki fingerprint create cheyadam.**

> **Symmetric = One shared secret key.**

> **Asymmetric = Public + Private key pair.**

> **Digital Signature = Integrity + signature verification.**

> **Certificate = Identity + Public Key binding.**

> **PKI = Keys + Certificates + CA + Trust + Validation.**

**Next:** Day 6 — Identity & Access Security (IAM, MFA, RBAC, ABAC, Privileged Access, Sessions).
