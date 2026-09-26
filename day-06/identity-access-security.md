# Day 6 — Identity & Access Security

## 🎯 Learning Goal

Understand how organizations control who can access systems, what they can access, and what actions they can perform.

Topics:
- Identity and Access Management (IAM)
- Authentication and Authorization
- MFA
- RBAC and ABAC
- Least Privilege
- Privileged Access
- Service Accounts
- Password and Session Security
- Identity attacks and defenses
- DevOps and DevSecOps identity security

> ⚠️ Practice only with accounts and systems you own or are authorized to test.

---

## 1. What is Identity and Access Security?

### 🇬🇧 English

Identity and Access Security protects digital identities and controls access to systems, applications, data, and resources.

The main questions are:
1. Who are you?
2. How do we verify you?
3. What are you allowed to access?
4. What actions are you allowed to perform?
5. When should access be removed?

### 🇮🇳 Tinglish

Simple ga:

> **Evaru system ni access cheyali? Vallaki em access undali? Eppudu access remove cheyali?**

ani control cheyadam Identity and Access Security.

## 2. Identity

An identity represents a person, service, device, application, or other entity that needs access to a resource.

Examples:
- Employee
- Administrator
- Application
- Service account
- Device
- CI/CD pipeline

### 🇮🇳 Tinglish

Identity ante human user matrame kaadu. Application, service account, device, and CI/CD pipeline kuda resources access cheyadaniki identity laga act cheyagalavu.

## 3. Authentication

Authentication verifies identity.

Examples:
- Password
- MFA
- Security key
- Certificate
- Biometrics
- SSH key

### 🇮🇳 Tinglish

Authentication question:
> **Nuvvu evaru?**

Username + Password → Authentication → Identity verified.

## 4. Authorization

Authorization determines what an authenticated identity is allowed to do.

Example:

User → Authenticated → Role / Policy → Read Reports ✅ → Delete Database ❌

### 🇮🇳 Tinglish

Authorization question:
> **Nuvvu em cheyagalavu?**

Login successful ayina ventane anni permissions automatically ravu.

## 5. Authentication vs Authorization

| Concept | Question | Example |
|---|---|---|
| Authentication | Who are you? | Password + MFA |
| Authorization | What can you do? | Read-only role |

🧠 Memory:
> Authentication = **Who?**
> Authorization = **What?**

## 6. MFA — Multi-Factor Authentication

MFA uses multiple authentication factors.

Common factors:
- Something you know → password/PIN
- Something you have → security key/authenticator
- Something you are → fingerprint/face

### 🇮🇳 Tinglish

Password okkate unte attacker password steal chesaka account access cheyagaladu. MFA add chesthe second factor kuda required.

Password + Second Factor → Access.

MFA account takeover risk ni reduce cheyadaniki important security control.

## 7. RBAC — Role-Based Access Control

RBAC assigns permissions through roles.

Example:

Developer → Read source code + Deploy to Dev
Support → Read support tickets
Admin → Administrative operations

### 🇮🇳 Tinglish

Prathi user ki permissions individually assign cheyyadam badulu role create chesi permissions assign cheyochu.

## 8. ABAC — Attribute-Based Access Control

ABAC makes access decisions using attributes such as:
- User
- Role
- Department
- Device
- Location
- Resource
- Time
- Risk/context

Example:
User = Finance AND Device = Managed AND Resource = Finance Data AND Time = Business Hours → Allow

### 🇮🇳 Tinglish

RBAC lo role important. ABAC lo multiple conditions and attributes consider chesi access decision tiskovachu.

> **Evaru? Ye department? Ye device? Ye resource? Ye time?**

## 9. Least Privilege

Least privilege means giving an identity only the access required to perform its job.

### 🇮🇳 Tinglish

> **Enta permission avasaram undo anta matrame ivvali.**

Unnecessary admin access ivvakudadhu. Account compromise ayithe excessive permissions impact ni increase chestayi.

## 10. Privileged Access

Privileged accounts can perform sensitive administrative operations.

Examples:
- Linux root
- Windows Administrator
- Domain Administrator
- Database administrator
- Cloud administrator

### 🇮🇳 Tinglish

Privileged account ante high-level operations cheyagalige account. These accounts need stronger controls and monitoring.

## 11. Privileged Access Management — PAM

PAM controls and monitors privileged access.

Important concepts:
- Just-in-time access
- Approval workflows
- Credential protection
- Session monitoring
- Privileged account inventory
- Least privilege

### 🇮🇳 Tinglish

Admin access permanent ga andariki ivvakunda requirement vachinappudu temporary privilege ivvadam safer approach.

## 12. Service Accounts

Applications and services often need identities to access resources.

Application → Service Account → Database

### 🇮🇳 Tinglish

Human user kakunda application kuda database/API/resource access cheyyali. Appudu service identity or service account use cheyochu.

Important: service account ki required permissions matrame ivvali.

## 13. Password Security

Good password security includes:
- Strong unique passwords
- Password managers
- MFA
- Password hashing
- Protection against credential reuse
- Monitoring compromised credentials

Applications should use dedicated password-hashing algorithms such as Argon2id, bcrypt, or scrypt.

### 🇮🇳 Tinglish

Same password multiple websites lo use chesthe one website leak ayina attacker other accounts try cheyochu.

> **Every important account ki unique password + MFA.**

## 14. Session Security

After authentication, applications often create a session.

Login → Authentication → Session → Authenticated Requests

Security concerns include:
- Session theft
- Session fixation
- Long-lived sessions
- Missing expiration
- Insecure cookies

### 🇮🇳 Tinglish

Login ayyaka prathi request ki password pampinchakunda application session/token use chestundi.

Attacker session token steal chesthe user laga act cheyadaniki chance untundi.

## 15. Secure Cookies

For web applications, important cookie protections include:
- Secure
- HttpOnly
- SameSite

### 🇮🇳 Tinglish

Session cookie sensitive information carry chesthe browser lo secure ga handle cheyyali.

Secure → HTTPS connection
HttpOnly → JavaScript access restriction
SameSite → Cross-site request controls

## 16. Common Identity Attacks

### Credential Stuffing
Using leaked username/password combinations against other services.

### Password Spraying
Trying a small number of common passwords across many accounts.

### Phishing
Tricking users into providing credentials or approving malicious actions.

### MFA Fatigue
Repeatedly sending authentication prompts hoping the user eventually approves one.

### Session Theft
Stealing a valid authenticated session.

### Privilege Abuse
Misusing excessive permissions.

### 🇮🇳 Tinglish

Attacker always password crack cheyyali ani rule ledu.

Leaked Password → Credential Stuffing → Account Access

or

Phishing → Credentials → Account Takeover

Identity security lo prevention + detection + response important.

## 17. Identity Security Detection

Security teams monitor signals such as:
- Repeated failed logins
- Successful login after many failures
- Unusual locations or devices
- New privileged account
- Privilege changes
- MFA changes
- Password resets
- Service-account anomalies

### 🇮🇳 Tinglish

Single event chusi attacker ani decide cheyyakudadhu. Multiple signals correlate cheyali.

Example:
Many Failed Logins → Successful Login → New Admin Privilege → Sensitive Resource Access → Investigation

## 18. DevOps Connection

Identity security is extremely important in DevOps.

Developer → Git → CI/CD → Cloud → Production

Important identities:
- Developer
- GitHub/GitLab user
- CI/CD runner
- Cloud role
- Kubernetes service account
- Application identity

### 🇮🇳 Tinglish

CI/CD pipeline ki unnecessary production admin permissions isthe pipeline compromise ayithe attacker production environment ki high privilege tho vellachu.

> **CI/CD identity ki least privilege.**

## 19. DevSecOps Connection

Identity security should be integrated into the software delivery lifecycle.

Developer → Git Repository → CI/CD Identity → Security Scans → Deployment Identity → Production

Important controls:
- MFA for human accounts
- Short-lived credentials where possible
- Secret management
- Least privilege
- Branch protection
- Protected environments
- Approval workflows
- Audit logging
- Service identity separation

### 🇮🇳 Tinglish

DevSecOps lo security scan okkate DevSecOps kaadu.

> **Evaru code push chestunnaru? Evaru deploy chestunnaru? Pipeline ki enta access undi? Production credentials ekkada unnayi?**

ivi kuda security questions.

## 20. Identity Lifecycle

Identity management is not only about creating users.

Join → Provision → Access → Review → Change Role → Revoke → Offboard

### 🇮🇳 Tinglish

Employee join ayinappudu account create chestam. Role change ayithe permissions update cheyali. Employee leave ayithe access revoke cheyali.

Old accounts active ga unte security risk.

## 21. Access Review

Organizations should periodically review:
- Who has access?
- Why do they have access?
- Is the access still required?
- Are privileged permissions justified?
- Are inactive accounts disabled?

### 🇮🇳 Tinglish

> **Ee user ki ee access ippatiki avasaram unda?**

Role change ayina tarvata old permissions remove cheyyakapothe privilege accumulation jaragachu.

## 22. Identity Security Checklist

- [ ] MFA enabled
- [ ] Strong unique passwords
- [ ] Password manager used where appropriate
- [ ] Least privilege applied
- [ ] Privileged accounts controlled
- [ ] Service accounts reviewed
- [ ] Inactive accounts disabled
- [ ] Access reviewed periodically
- [ ] Sessions protected
- [ ] Secure cookie settings reviewed
- [ ] Login anomalies monitored
- [ ] Privilege changes monitored
- [ ] Secrets not hardcoded
- [ ] CI/CD identities use least privilege
- [ ] Offboarding access revoked

# 🧪 Day 6 Hands-on Lab

## Linux

Run:

    whoami
    id
    groups

Review sudo privileges:

    sudo -l

Do not modify sudo configuration during this lab.

## Windows

Run:

    whoami
    whoami /all
    net user
    net localgroup Administrators

Review the output and identify:
- Current user
- Groups
- Privileges
- Administrative membership

## Web Session Lab

Use a local or authorized web application and inspect browser developer tools.

Look at Application → Cookies → Session-related cookies.

Check whether security attributes such as Secure, HttpOnly, and SameSite are present where appropriate.

Do not capture or share real session tokens.

# 🎯 Day 6 Mini Challenge

Answer these without looking at the notes:
1. Authentication vs authorization?
2. What is MFA?
3. What is RBAC?
4. What is ABAC?
5. What is least privilege?
6. What is PAM?
7. Why are service accounts sensitive?
8. What is credential stuffing?
9. What is password spraying?
10. What is MFA fatigue?
11. Why are sessions security-sensitive?
12. Why should CI/CD identities have limited permissions?
13. What should happen to an employee access during offboarding?
14. Why should access be reviewed periodically?

# 🎤 Interview Questions

### Q1. What is IAM?

**English:** Identity and Access Management is the set of processes and controls used to manage identities and control access to resources.

**Tinglish:** Users and identities ni manage chesi, vallaki required resources ki correct access ivvadam IAM.

### Q2. What is MFA?

**English:** Multi-factor authentication requires authentication using multiple factor categories.

**Tinglish:** Password tho paatu second authentication factor use chesi account security increase cheyadam MFA.

### Q3. RBAC vs ABAC?

**English:** RBAC makes access decisions primarily through roles, while ABAC uses attributes and policies.

**Tinglish:** RBAC = role based access. ABAC = user, resource, device, location, time lanti attributes base chesi access decision.

### Q4. What is least privilege?

**English:** Least privilege gives an identity only the permissions necessary for its required tasks.

**Tinglish:** User ki required work ki enta permission avasaram undo anta matrame ivvadam.

### Q5. What is credential stuffing?

**English:** Credential stuffing uses previously leaked username/password combinations against other services.

**Tinglish:** Vere website leak ayina username/password combinations ni other websites lo try cheyadam credential stuffing.

### Q6. Why are service accounts important in DevSecOps?

**English:** Service accounts allow automation and applications to access resources, so excessive permissions can create significant security risk if compromised.

**Tinglish:** CI/CD or application service account compromise ayithe attacker automated access use chesi sensitive resources reach avvachu. Anduke least privilege important.

# 🧠 Day 6 Summary

Identity → Authentication → MFA → Authorization → RBAC / ABAC → Least Privilege → Privileged Access → Service Accounts → Session Security → Identity Threats → Monitoring → DevOps Identity → DevSecOps Identity → Access Lifecycle

## 🇮🇳 Final Tinglish Memory

> **Identity Security ante “Evaru?” → Authentication, “Em cheyagalru?” → Authorization, “Enta access ivvali?” → Least Privilege, “High privilege ni ela control cheyali?” → PAM, “Suspicious access ni ela detect cheyali?” → Monitoring.**

**Next:** Day 7 — Vulnerability, Threat, Risk & Vulnerability Management.
---
# 🔥 Extra Real-World Examples & Complete Interview Coverage

## Practical Examples
### RBAC
Developer role → read source code + deploy to development. The role is assigned to multiple developers.
### ABAC
User = Finance + managed device + finance resource + business hours → allow.
### Least privilege
CI/CD should not automatically have permanent production-admin permissions.
### Account lifecycle
Join → Provision → Review → Role Change → Revoke → Offboard.
**Tinglish:** Employee leave ayyaka access active ga unte unnecessary risk.

## 🎤 Interview Question Bank
1. What is IAM?
2. Identity vs account?
3. Authentication vs authorization?
4. What is MFA?
5. What are authentication factors?
6. What is RBAC?
7. What is ABAC?
8. RBAC vs ABAC?
9. What is least privilege?
10. What is privileged access?
11. What is PAM?
12. What is a service account?
13. Why are service accounts sensitive?
14. What is credential stuffing?
15. What is password spraying?
16. What is phishing?
17. What is MFA fatigue?
18. What is session theft?
19. What is session fixation?
20. Why are Secure, HttpOnly and SameSite cookie attributes important?
21. What is access review?
22. What is identity lifecycle management?
23. Why should inactive accounts be disabled?
24. Why should CI/CD identities use least privilege?
25. What are short-lived credentials?
26. Why should privileged accounts be monitored?
27. What is privilege accumulation?
28. A developer can delete production data. What would you review?
29. A service account has full admin permissions. What is the concern?
30. A CI/CD token has broad production permissions. How would you reduce risk?

**Interview formula:** Who → Verify → What access → Why access → Monitor → Revoke.
