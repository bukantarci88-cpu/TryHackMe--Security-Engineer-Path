# Eng 6.1. OWASP Top 10 2025: IAAA Failures and API

#### **OWASP Top 10 2025: IAAA Failures**

#### **Task 1 - Introduction**

The following categories are covered in this room:

1. A01: Broken Access Control
2. A07: Authentication Failures
3. A09: Logging & Alerting Failures

#### **Task 2 - What is IAAA?**

IAAA is a simple way to think about how users and their actions are verified on applications. Each item plays a crucial role and it isn't possible to skip a level. That means, if a previous item isn't being performed, you cannot perform the later times. The four items are:

- **Identity** - the unique account (e.g., user ID/email) that represents a person or service.
- **Authentication** - proving that identity (passwords, OTP, passkeys).
- **Authorisation** - what that identity is allowed to do.
- **Accountability** - recording and alerting on who did what, when, and from where.

**Answer the questions below**
What does IAAA stand for? Identity, Authentication, Authorisation, Accountability

#### **Task 3 - A01: Broken Access Control**

Broken Access Control happens when the server doesn’t properly enforce **who can access what** on every request. A common occurence of this is **IDOR** (Insecure Direct Object Reference): if changing an ID (like `?id=7 → ?id=6`) lets you see or edit someone else’s data, access control is broken.

**Answer the questions below**
If you don't get access to more roles but can view the data of another users, what type of privilege escalation is this? Horizontal
What is the note you found when viewing the user's account who had more than $ 1 million? THM{Found.the.Millionare!} 

<img width="905" height="492" alt="image" src="https://github.com/user-attachments/assets/2d2f8f38-ecbf-4aff-b413-ef44f31ba31d" />


#### **Task 4 - A07: Authentication Failures**

Authentication Failures happen when an application can’t reliably verify or bind a user’s identity. Common issues include:

- username enumeration
- weak/guessable passwords (no lockout/rate limits)
- logic flaws in the login/registration flow
- insecure session or cookie handling

**Answer the questions below**
What is the flag on the admin user's dashboard? THM{Account.confusion.FTW!}

<img width="746" height="553" alt="image 1" src="https://github.com/user-attachments/assets/a6fa4610-c0c9-45bb-be10-53b0d903ba42" />

#### **Task 5 - A09: Logging & Alerting Failures**

Without proper logging and alerting, security teams may miss attacks or struggle to investigate incidents. Missing authentication logs, lack of alerts for suspicious activity, poor log retention, and tamperable logs can leave organizations blind to threats. Effective logging provides accountability and visibility, helping defenders detect, investigate, and respond to attacks faster.

**Answer the questions below**
It looks like an attacker tried to perform a brute-force attack, what is the IP of the attacker? 203.0.113.45

<img width="913" height="263" alt="image 2" src="https://github.com/user-attachments/assets/a162d266-e4f3-442a-8b29-5dc7bfa6bf3a" />

Looks like they were able to gain access to an account! What is the username associated with that account? admin

What action did the attacker try to do with the account? List the endpoint the accessed. /supersecretadminstuff

<img width="900" height="262" alt="image 3" src="https://github.com/user-attachments/assets/620ea5b7-2f44-402b-b604-a87c246930ca" />


#### **Task 6 - Conclusion**

Understanding Identity, Authentication, Authorization, and Accountability is essential for securing web applications.

✅ **A01: Broken Access Control** – Enforce server-side authorization checks on every request.

✅ **A07: Authentication Failures** – Protect against brute-force attacks, enforce unique identities, and rotate sessions after password or privilege changes.

✅ **A09: Logging & Alerting Failures** – Log authentication events, centralize logs, and alert on suspicious activities such as brute-force attempts and privilege escalation.

Strong access controls, secure authentication, and effective monitoring form the foundation of application security.

#### **Task 7 - API in Cybersecurity**

In cybersecurity, an **API (Application Programming Interface)** is both a **critical asset** and a **common attack surface**. APIs allow systems, applications, and services to communicate—but if they are not properly secured, they can expose sensitive data and functionality to attackers.

**Why APIs Matter in Cybersecurity:** Modern applications (web apps, mobile apps, cloud services) heavily rely on APIs for:

- User authentication (login systems)
- Data exchange (databases, microservices)
- Payment processing
- Third-party integrations (Google, payment gateways, etc.)

Because APIs often expose direct access to backend systems, they are a **high-value target for attackers**.

**Common API Security Risks:** According to security research such as OWASP, APIs are vulnerable to:

**1. Broken Authentication:** Weak login or token systems allow attackers to impersonate users.

**2. Broken Authorization (BOLA / IDOR):** Users can access data they should not (e.g., changing an ID in the URL).

**3. Excessive Data Exposure:** APIs return more data than necessary (e.g., passwords, internal fields).

**4. Injection Attacks:** Malicious input (SQL, NoSQL, command injection) sent through API requests.

**5. Rate Limiting Issues:** No limits → attackers can brute force or abuse endpoints.

**Example Attack Scenario**

```
GET /api/user/1001
```

If the API does not check permissions properly, an attacker might change it to:

```
GET /api/user/1002
```

→ This can expose another user’s private data (**IDOR vulnerability**).

**How to Secure APIs**

**1. Strong Authentication**

- Use OAuth 2.0, JWT tokens, or API keys
- Avoid weak or predictable tokens

**2. Proper Authorization**

- Enforce role-based access control (RBAC)
- Validate every request

**3. Input Validation**

- Sanitize all inputs
- Prevent injection attacks

**4. Rate Limiting**

- Prevent brute-force and abuse

**5. HTTPS Everywhere**

- Encrypt data in transit

**6. API Gateway Protection**

- Centralized security, logging, and filtering

**OWASP API Security Top Risks**

Some of the most important API risks identified by OWASP include:

- Broken Object Level Authorization
- Broken Authentication
- Excessive Data Exposure
- Lack of Resources & Rate Limiting
- Security Misconfiguration

Shortly in cybersecurity, APIs are **critical communication bridges**, but also **one of the most targeted attack surfaces**. Securing APIs is essential to protect modern applications from data leaks, unauthorized access, and abuse.

**What is `application/json`?**

**`application/json`** is a **MIME type (media type)** used in HTTP requests and responses to indicate that the data format is **JSON (JavaScript Object Notation)**.

It tells the server or client:

👉 “The data being sent or received is in JSON format.”

**Where it is used in Cybersecurity & Web APIs**

In APIs, especially in web security testing (like in Burp Suite or `curl`), you often see:

- Request headers
- API responses
- POST/PUT requests

**Example HTTP Request**

```
POST /api/login HTTP/1.1
Content-Type: application/json
```

Body:

```
{
  "username":"admin",
  "password":"1234"
}
```

**Why it is important in Cybersecurity**

Attackers and security testers analyze `application/json` because:

- APIs often expose sensitive data through JSON
- JSON inputs can be vulnerable to:
    - Injection attacks
    - Broken authentication
    - IDOR (Insecure Direct Object Reference)
- Improper validation of JSON input can lead to exploitation

**Example using curl**

```
curl-X POST https://example.com/api/login \
-H"Content-Type: application/json" \
-d'{"username":"admin","password":"1234"}'
```

**Summary**

- `application/json` = tells the system data is in JSON format
- Used heavily in APIs and web applications
- Very important in cybersecurity for testing and analyzing API behavior

