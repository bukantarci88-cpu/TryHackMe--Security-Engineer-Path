# Eng 6.2. OWASP Top 10 2025: Application Design Flaws

#### **OWASP Top 10 2025: Application Design Flaws**

#### **Task 1 - Introduction**

The following categories are covered in this room:

1. AS02: Security Misconfigurations
2. AS03: Software Supply Chain Failures
3. AS04: Cryptographic Failures
4. AS06: Insecure Design

#### **Task 2 - AS02: Security Misconfigurations**

Security misconfigurations occur when systems, applications, or cloud services are deployed with unsafe defaults, excessive permissions, or exposed services. These setup mistakes can create easy opportunities for attackers. A well-known example is the 2017 Uber breach, where a publicly accessible AWS S3 bucket exposed sensitive user and driver data.

The lesson: secure configurations, regular reviews, and least-privilege access are just as important as secure code.

**Common Patterns**

- Default credentials or weak passwords left unchanged
- Unnecessary services or endpoints exposed to the internet
- Misconfigured cloud storage or permissions (S3, Azure Blob, GCP buckets)
- Unrestricted API access or missing authentication/authorisation
- Verbose error messages exposing stack traces or system details
- Outdated software, frameworks, or containers with known vulnerabilities
- Exposed AI/ML endpoints without proper access controls

**How To Prevent It**

- Harden default configurations and remove unused features or services
- Enforce strong authentication and least privilege across all systems
- Limit network exposure and segment sensitive resources
- Keep software, frameworks, and containers up to date with patches
- Hide stack traces and system information from error messages
- Audit cloud configurations and permissions regularly
- Secure AI endpoints and automation services with proper access controls and monitoring
- Integrate configuration reviews and automated security checks into your deployment pipeline

**Challenge:** Navigate to `MACHINE_IP:5002`. It appears that the developers left too many traces in their User Management APIs.

**Answer the questions below**
What's the flag? THM{V3RB0S3_3RR0R_L34K}

<img width="1765" height="762" alt="image 2" src="https://github.com/user-attachments/assets/aa82f300-b5fa-4647-ba56-b08db710a43c" />
<img width="945" height="726" alt="image 1" src="https://github.com/user-attachments/assets/677d07cc-94ed-4860-8bba-fe777d4ba69f" />
<img width="887" height="252" alt="image" src="https://github.com/user-attachments/assets/00b3e050-a3f8-48ce-ad0a-b82b0c503cdc" />


#### **Task 3 - AS03: Software Supply Chain Failures**

Modern applications rely heavily on third-party libraries, APIs, and AI models. When these dependencies are compromised, outdated, or improperly verified, attackers can exploit them to gain access without targeting your code directly. The 2021 SolarWinds incident demonstrated how a trusted software update can become a vehicle for a large-scale supply chain attack.

Key takeaway: Continuously verify dependencies, monitor third-party components, and secure the software supply chain to reduce risk.

**Common Patterns**

- Using unverified or unmaintained libraries and dependencies
- Automatically installing updates without verification
- Over-reliance on third-party AI models without monitoring or auditing
- Insecure build pipelines or CI/CD processes that allow tampering
- Poor license or provenance tracking for components
- Lack of monitoring for vulnerabilities in dependencies after deployment

**How To Protect The Supply Chain**

- Verify all third-party components, libraries, and AI models before use
    
    
- Monitor and patch dependencies regularly
- Sign, verify, and audit software updates and packages
- Lock down CI/CD pipelines and build processes to prevent tampering
- Track provenance and licensing for all dependencies
- Implement runtime monitoring for unusual behaviour from dependencies or AI components
- Integrate supply chain threat modelling into the SDLC, including testing, deployment, and update workflows

**Challenge:** Navigate to `MACHINE_IP:5003`. The code is outdated and imports an old `lib/vulnerable_utils.py` component. Can you ***debug*** it?

**Answer the questions below**
What's the flag? THM{SUPPLY_CH41N_VULN3R4B1L1TY}


<img width="1042" height="777" alt="image 3" src="https://github.com/user-attachments/assets/0510ddd8-aeb0-49d1-8534-fbfbfa7c2356" />


#### **Task 4 - AS04: Cryptographic Failures**

Cryptographic failures occur when sensitive data is not properly protected through encryption. Common issues include weak algorithms, hard-coded keys, poor key management, and storing data without encryption. When cryptography fails, attackers may gain access to passwords, tokens, personal information, and other sensitive data through techniques such as man-in-the-middle attacks or brute-forcing weak keys.

The key takeaway: use strong encryption, protect cryptographic keys, and secure sensitive data both in transit and at rest.

**Common Patterns**

- Using deprecated or weak algorithms like MD5, SHA-1, or ECB mode
- Hard-coded secrets in code or configuration
- Poor key rotation or management practices
- Lack of encryption for sensitive data at rest or in transit
- Self-signed or invalid TLS certificates
- Using AI/ML systems without proper secret handling for model parameters or sensitive inputs

**How To Prevent It**

- Use strong, AES modern algorithms such as GCM, ChaCha20-Poly1305, or enforce TLS 1.3 with valid certificates
- Use secure key management services like Azure Key Vault, AWS KMS, or HashiCorp Vault
- Rotate secrets and keys regularly, following defined crypto periods
- Document and enforce policies and standard operating procedures for key lifecycle management
- Maintain a complete inventory of certificates, keys, and their owners
- Ensure AI models and automation agents never expose unencrypted secrets or sensitive data
- The web application in this room contains a weakness of this type for you to explore.

**Challenge:** Navigate to `MACHINE_IP:5004`. Can you find the key to decrypt the file?

<img width="750" height="375" alt="image 4" src="https://github.com/user-attachments/assets/8cdf176d-9078-4080-a9c4-4afef4688995" />


**Answer the questions below**
What's the flag? THM{CRYPTO_FAILURE_H4RDCOD3D_K3Y}

<img width="1373" height="502" alt="image 5" src="https://github.com/user-attachments/assets/cb65dadd-2baf-4ac7-917a-2e50a97629aa" />


#### **Task 5 - AS06: Insecure Design**

Insecure design occurs when security weaknesses are built into an application's architecture or logic from the beginning. These issues often result from missing threat modelling, poor design reviews, or incorrect assumptions about system behaviour. With AI-powered systems, insecure design risks increase when developers assume AI outputs are always safe or fail to add proper controls around generated code, queries, and decisions.

A key lesson: security must be designed into systems from the start. Architecture reviews, threat modelling, and secure design principles are essential.

**Common Insecure Designs In 2025**

- Weak business logic controls, like recovery or approval flows
- Flawed assumptions about user or model behaviour
- AI components with unchecked authority or access
- Missing guardrails for LLMs and automation agents
- Test or debug bypasses left in production
- No consistent abuse-case review or AI threat modelling

**Insecure Design In The AI Era**

AI introduces new security challenges caused by poor design decisions. Prompt injection can manipulate AI behavior, blind trust in model outputs can create unsafe automation, and unverified models or datasets can introduce hidden backdoors.

The key lesson: AI systems need secure architecture, input validation, model verification, and human oversight to reduce risks.

**How To Design Securely**

- Treat every model as untrusted until proven otherwise.
- Validate and filter all model inputs and outputs to ensure accuracy and integrity.
- Separate system prompts from user content.
- Keep sensitive data out of prompts unless absolutely needed and protect it with strict controls.
- Require human review for high-risk AI actions.
- Log model provenance, monitor behaviour, and apply differential privacy for sensitive data.
- Include specific threat modelling for prompt attacks,AI inference risks, agent misuse, and supply chain compromise throughout the design process.
- Build threat modelling into every stage of development, not just at the start.
- Define clear security requirements for each feature before implementation.
- Apply the principle of least privilege across users, APIs, and services.
- Ensure proper authentication, authorisation, and session management across the system.
- Keep dependencies, third-party components, and supply chain sources verified and up to date.
- Continuously monitor and test the system for logic flaws, abuse paths, and emergent risks as new features or AI components are added.

**Challenge:** Navigate to `MACHINE_IP:5005`. Have they assumed that only mobile devices can access it?

**Answer the questions below**
What's the flag? THM{1NS3CUR3_D35IGN_4SSUMPT10N}

<img width="677" height="426" alt="image 8" src="https://github.com/user-attachments/assets/b304904a-1342-4971-a892-f9eefd121e37" />
<img width="867" height="245" alt="image 7" src="https://github.com/user-attachments/assets/b4416795-e760-4210-b276-70ba3496b183" />
<img width="726" height="547" alt="image 6" src="https://github.com/user-attachments/assets/70fd1a6b-0aaf-4dd8-adf4-433645f5ef9e" />


#### **Task 6 - Conclusion**

Security issues such as **Security Misconfigurations, Software Supply Chain Failures, Cryptographic Failures, and Insecure Design** share one common root cause: weak security foundations. Security cannot be added as an afterthought. Strong systems require:

✅ Secure design principles

✅ Proper threat modelling

✅ Safe configurations

✅ Trusted dependencies

✅ Strong cryptographic practices

The key lesson: build security from the beginning, question default settings, and continuously evaluate risks across the entire application lifecycle.

![Gemini_Generated_Image_3m8oi63m8oi63m8o.png](Eng%206%202%20OWASP%20Top%2010%202025%20Application%20Design%20Flaws/Gemini_Generated_Image_3m8oi63m8oi63m8o.png)
