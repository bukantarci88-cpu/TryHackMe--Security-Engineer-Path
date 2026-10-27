# Eng 6.3. OWASP Top 10 2025: Insecure Data Handling

#### **OWASP Top 10 2025: Insecure Data Handling**

#### **Task 1 - Introduction**

In this room, you will learn about the elements relating to application behaviour and user input. 

- A04: Cryptographic Failures
- A05: Injection
- A08: Software or Data Integrity Failures

#### **Task 2 - A04: Cryptographic Failures**

Cryptographic failures occur when sensitive data is not properly protected due to missing encryption, weak algorithms, poor key management, or insecure implementations. Common issues include:
• Storing passwords without secure hashing
• Using outdated algorithms like MD5, SHA1, or DES
• Exposing encryption keys or credentials
• Creating custom cryptographic solutions instead of using trusted standards

Best practices:
✅ Use strong modern algorithms
✅ Hash passwords with bcrypt, scrypt, or Argon2
✅ Use trusted security libraries
✅ Store secrets securely with proper key management systems

Strong cryptography protects sensitive data and prevents unauthorized access.

**Practical:** This web app demonstrates a "note sharing" service that uses a weak, shared derivative key to protect the notes.

**Answer the questions below**
Decrypt the encrypted notes. One of them will contain a flag value. What is it? THM{WEAK_CRYPTO_FLAG}

<img width="1241" height="415" alt="image" src="https://github.com/user-attachments/assets/a4ecaed9-2c39-4b5b-bb9d-8cba289bd769" />


#### **Task 3 - A05: Injection**

Injection occurs when applications process untrusted user input in an unsafe way, allowing attackers to execute unintended commands or queries.

Common injection attacks include:
• SQL Injection
• Command Injection
• Server-Side Template Injection (SSTI)
• AI Prompt Injection

Prevention requires treating all user input as untrusted:
✅ Use prepared statements and parameterized queries
✅ Avoid passing user input directly to system commands
✅ Validate, sanitize, and properly handle input
✅ Use secure APIs instead of unsafe processing methods

Secure input handling is essential to prevent attackers from manipulating application logic.

**Practical:** This example illustrates Server Side Template Injection (SSTI).  

**Answer the questions below**
Perform an SSTI attack on the practical. You need to read the contents of flag.txt that is located within the same directory as the web application. THM{SSTI_FLAG_OBTAINED}

#### **Task 4 - A08: Software or Data Integrity Failures**

Software or Data Integrity Failures occur when applications trust code, updates, or data without verifying their authenticity, integrity, or source.

Common risks include:
• Unverified software updates
• Loading scripts or configurations from untrusted sources
• Accepting modified files, binaries, or data without validation
• Weak integrity controls in CI/CD pipelines

Prevention requires establishing strong trust boundaries:
✅ Verify software and update integrity using cryptographic checks
✅ Allow modifications only from trusted sources
✅ Secure build and deployment pipelines
✅ Validate critical data before use

Never blindly trust code or data—always verify its integrity.

**Practical:** This practical will demonstrate a deserialization attack in Python.  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/5de96d9ca744773ea7ef8c00-1763110949029.svg)

<img width="777" height="460" alt="image 1" src="https://github.com/user-attachments/assets/caf7cb8c-29cc-4ede-b6da-017849bf54b7" />


**Answer the questions below**
Use Python to pickle a malicious, serialised payload that reads the contents of flag.txt and submits it to the application. 

What are the contents of flag.txt? THM{INSECURE_DESERIALIZATION}

<img width="773" height="713" alt="image 5" src="https://github.com/user-attachments/assets/08ab8b2d-efb6-4588-9feb-20e75502f5c5" />
<img width="1337" height="148" alt="image 4" src="https://github.com/user-attachments/assets/7bb14adc-2e90-4771-ad39-220179872b1b" />
<img width="1206" height="708" alt="image 3" src="https://github.com/user-attachments/assets/e002c76e-285f-426c-9699-b26e7251f3dc" />


(run) python3.9 pickle_gen.py
(run it again after edited payloads)

<img width="1453" height="183" alt="image 7" src="https://github.com/user-attachments/assets/b44b9725-8206-4f81-8be7-48a5570d2445" />
<img width="1218" height="725" alt="image 6" src="https://github.com/user-attachments/assets/eb79ae52-e320-4dde-9f79-0302608f1467" />


