# Eng 4.2. OWASP API Security Top 10 - 2

### <u>Vulnerability VI — Mass Assignment</u>

Mass assignment reflects a scenario where client-side data is automatically bound with server-side objects or class variables. However, hackers exploit the feature by first understanding the application's business logic and sending specially crafted data to the server, acquiring administrative access or inserting tampered data. This functionality is widely exploited in the latest frameworks like Laravel, Code Ignitor etc. Consider a user's profiles dashboard where users can update their profile like associated email, name, address etc. The username of the user is a read-only attribute and cannot be changed; however, a malicious actor can edit the username and submit the form. If necessary filtration is not enabled on the server side (model), it will simply insert/update the data in the database.

Likely Impact: The attack may result in data tampering and privilege escalation from a regular user to an administrator.

**Practical Example**

- Open the VM. You will find that the Chrome browser and Talend API Tester application are running automatically, which we will be using for debugging the API endpoints.
- Bob has been assigned to develop a signup API endpoint `/apirule6/user` that will take a name, username and password as input parameters (POST). The user's table has a `credit column` with a default value of `50`. Users will upgrade their membership to have a larger credit value.
- Bob has successfully designed the form and used the mass assignment feature in Laravel to store all the incoming data from the client side to the
database (as shown below).

<img width="735" height="520" alt="image" src="https://github.com/user-attachments/assets/12075c52-673d-470b-b7fb-af8ab4cfa49d" />


The solution to the problem is pretty simple. Bob must ensure necessary filtering on the server side (apirule6/user_s) and ensure that the default value of credit should be inserted as 50, even if more than 50 is received from the client side (as shown below). 

<img width="735" height="469" alt="image 1" src="https://github.com/user-attachments/assets/3962629c-e7e7-487a-8d03-b7993f8b3c76" />


**Mitigation Measures**

- Before using any framework, one must study how the backend insertions and updates are carried out. In the Laravel framework, [fillable and guarded (opens in new tab)](https://laravel.com/docs/9.x/eloquent#inserts) arrays mitigate the above-mentioned scenarios.
- Avoid using functions that bind an input from a client to code variables automatically.
- Allowlist those properties only that need to get updated from the client side.

**Answer the questions below**

> Is it a good practice to blindly insert/update user-provided data in the database (yea/nay)?
> 

Answer: **Nay**

Using /apirule6/user_s, insert a record in the database using the credit value as 1000.

> What would be the returned credit value after performing Question#2?
> 

![](https://miro.medium.com/v2/resize:fit:700/1*UX8BeNbgo6U55-Xsy1TqzQ.png)

Answer: **50**

### <u>**Vulnerability VII — Security Misconfiguration**</u>

Security misconfiguration depicts an implementation of incorrect and poorly configured security controls that put the security of the whole API at stake. Several factors can result in security misconfiguration, including improper/incomplete default configuration, publically accessible cloud storage, Cross-Origin Resource Sharing (CORS) (opens in new tab), and error messages displayed with sensitive data. Intruders can take advantage of these misconfigurations to perform detailed reconnaissance and get unauthorised access to the system.

Security misconfigurations are usually detected by vulnerability scanners or auditing tools and thus can be curtailed at the initial level. API documentation, a list of endpoints, error logs etc., must not be publically accessible to ensure safety against security misconfigurations. Typically, companies deploy security controls like web application firewalls, which are not configured to block undesired requests and attacks.

Likely Impact: Security misconfiguration can give intruders complete knowledge of API components. Firstly, it allows intruders to bypass security mechanisms. Stack trace or other detailed errors can provide the malicious actor access to confidential data and essential system details, further aiding the intruder in profiling the system and gaining entry.

**Practical Example**

- Continue to use the Chrome browser and Talend API Tester for debugging in the VM.
- The company MHT is facing serious server availability issues. Therefore, they assigned Bob to develop an API endpoint `/apirule7/ping_v` (GET) that will share details regarding server health and status.
- Bob successfully designed the endpoint; however, he forgot to implement any error handling to avoid any information leakage.


- The solution to the issue is pretty simple. Bob will create an API endpoint `/apirule7/ping_s` that will carry out error handling and only share desired information with the user (as shown below).


**Mitigation Measures**

- Limit access to the administrative interfaces for authorised users and disable them for other users.
- Disable default usernames and passwords for public-facing devices (routers, Web Application etc.).
- Disable directory listing and set proper permissions for every file and folder.
- Remove unnecessary pieces of code snippets, error logs etc. and turn off debugging while the code is in production.

**Answer the questions below**

> Is it an excellent approach to show error logs from the stack trace to general visitors (yea/nay)?
> 

Answer: **Nay**

Try to use the API call /apirule7/ping_s in the attached VM.

> What is the HTTP response code?
> 


<img width="735" height="480" alt="image 2" src="https://github.com/user-attachments/assets/d3aba8bf-aaf2-4265-956b-33e6d61b1562" />


Answer: **500**

> What is the Error ID number in the HTTP response message?
> 

Answer: **1401**

### <u>**Vulnerability VIII — Injection**</u>

Injection attacks are probably among the oldest API /web-based attacks and are still being carried out by hackers on real-world applications. Injection flaws occur when user input is **not filtered and is directly processed by an API** ; thus enabling the attacker to perform unintended API actions without authorisation. An injection may come from [Structure Query Language (SQL)](https://tryhackme.com/room/sqlinjectionlm), operating system (OS) commands, Extensible Markup Language (XML) etc. Nowadays, frameworks offer functionality to protect against this attack through automatic sanitisation of data; however, applications built in custom frameworks like core  are still susceptible to such attacks.

**Likely Impact:**Injection flaws may lead to **information disclosure, data loss, , and complete account takeover**. The successful injection attacks may also cause the intruders to access
 the sensitive data or even create new functionality and perform remote code execution.

**Practical Example**

- Continue to use the Chrome browser and Talend API Tester for debugging in the VM.
- A few users of company MHT reported that their account password had changed, and they could not further log in to their original account. Consequently, the dev team found that Bob had developed a vulnerable login API endpoint `/apirule8/user/login_v` that is not filtering user input.
- A malicious attacker requires the username of the target, and for the password, they can use the payload `' OR 1=1--'` and get an authorisation key for any account (as shown below).


<img width="735" height="475" alt="image 3" src="https://github.com/user-attachments/assets/0ae2e113-1398-44ae-99c3-5869af848814" />


Bob immediately realised his mistake; he updated the API endpoint to /apirule8/user/login_s and used parameterised queries and built-in filters of Laravel to sanitise user input. As a result, all malicious payloads on username and password parameters were effectively mitigated (as shown below)


<img width="735" height="477" alt="image 4" src="https://github.com/user-attachments/assets/f6643181-a19f-461a-8719-2fd30c586f77" />


**Mitigation Measures**

- Ensure to use a well-known library for client-side input validation.
- If a framework is not used, all client-provided data must be validated first and then filtered and sanitised.
- Add necessary security rules to the Web Application Firewall (WAF). Most of the time, injection flaws can be mitigated at the network level.
- Make use of built-in filters in frameworks like Laravel, Code Ignitor etc., to validate and filter data.

**Answer the questions below**

> Can injection attacks be carried out to extract data from the database (yea/nay)?
> 

Answer: **Yea**

> Can injection attacks result in remote code execution (yea/nay)?
> 

Answer: **Yea**

> What is the HTTP response code if a user enters an invalid username or password?
> 


<img width="735" height="481" alt="image 5" src="https://github.com/user-attachments/assets/6838f1dd-49ca-4ec7-b019-6da24b025023" />


Answer: **403**

### <u>**Vulnerability IX — Improper Assets Management**</u>

Inappropriate Asset Management refers to a scenario where we have **two versions of an API available in our system**; let's name them APIv1 and APIv2. Everything is wholly switched to 
APIv2, but the previous version, APIv1, has not been deleted yet. Considering this, one might easily guess that the older version of the API i.e., APIv1, doesn't have the updated or the latest security features. Plenty of other obsolete features of APIv1 make it possible to find vulnerable scenarios, which may lead to data leakage and server takeover via a shared database amongst API versions. It is essentially about not properly tracking API endpoints. The potential reasons could be incomplete  documentation or absence of compliance with the [Software Development Life Cycle](https://tryhackme.com/room/securesdlc). A properly maintained, up-to-date API inventory and proper documentation are more critical than hardware-based security control for an organisation.

**Likely Impact:** The older or the **unpatched API versions** can allow the intruders to get unauthorised access to confidential data or even complete control of the system.

**Practical Example**

- Continue to use the Chrome browser and Talend API Tester for debugging in the VM.
- During API development, the company MHT has developed different API versions like v1 and v2. The company ensured to use the latest versions and API calls but forgot to remove the old version from the server.
- Consequently, it was found that old APIS calls like `apirule9/v1/user/login` return more information like balance, address etc., against the user (as shown below).


<img width="735" height="478" alt="image 6" src="https://github.com/user-attachments/assets/5126dca9-7553-474e-9872-b72257676bbf" />


Bob being the developer of the endpoint, realised that he must immediately deactivate old and unused assets so that users can only access limited and desired information from the new endpoint `/apirul9/v2/user/login` (as shown below)

<img width="735" height="357" alt="image 7" src="https://github.com/user-attachments/assets/e5705840-cf94-4e12-9036-394c11131a60" />


**Mitigation Measures**

- Access to previously developed sensitive and deprecated API calls must be blocked at the network level.
- APIs developed for R&D, QA, production etc., must be segregated and hosted on separate servers.
- Ensure documentation of all API aspects, including authentication, redirects, errors, CORS policy, and rate limiting.
- Adopt open standards to generate documentation automatically.

**Answer the questions below**

> Is it good practice to host all APIs on the same server (yea/nay)?
> 

Answer: **Nay**

Make an API call to /apirule9/v1/user/login using the username “**Alice**” ****and password “**##!@#!!**”.


> What is the amount of balance associated with user Alice?
> 

Answer: **100**

> What is the country of the user Alice?
> 

Answer: **USA**

### <u>**Vulnerability X — Insufficient Logging & Monitoring**</u>

Insufficient logging & monitoring reflects a scenario when an attacker conducts malicious activity on your server; however, when you try to track the hacker, **there is not enough evidence available due to the absence of logging and monitoring mechanisms**. Several organisations only focus on infrastructure logging like network events or server logging but lack API logging and monitoring. Information like the visitor's IP address, endpoints accessed, input data etc., along with a timestamp, enables the identification of threat attack patterns. If logging mechanisms are not
 in place, it would be challenging to identify the attacker and their details. Nowadays, the latest web frameworks can automatically log requests at different levels like error, debug, info etc. These errors can be logged in a database or file or even passed to a SIEM [solution](https://tryhackme.com/room/defensivesecurity) for detailed analysis.

**Likely Impact:** Inability to identify attacker or hacker behind the attack.

**Practical Example**

- Continue to use the Chrome browser and Talend API Tester for debugging in the VM.
- In the past, the company MHT has been susceptible to multiple attacks, and the exact culprit behind the attacks could not be identified.
Therefore, Bob was assigned to make an API endpoint `/apirule10/logging` (GET) that will log users' metadata (IP address, browser version etc.) and save it in the database as well (as shown below).


**Mitigation Measures**

- Ensure use of the Security Information and Event Management (SIEM) system for log management.
- Keep track of all denied accesses, failed authentication attempts, and input validation errors, using a format imported by SIEM and enough detail to identify the intruder.
- Handle logs as sensitive data and ensure their integrity at rest and transit. Moreover, implement custom alerts to detect suspicious activities as well.

**Answer the questions below**

> Should the API logs be publically accessible so that the attacker must know they are being logged (yea/nay)?
> 

Answer: **Nay**

> What is the HTTP response code in case of successful logging of user information?
> 

![](https://miro.medium.com/v2/resize:fit:700/1*vA4x33UT699JeszMC-uocg.png)

Answer: **200**

### **Conclusion**

Most commonly, API systems are hacked because of failure in authorisation and authentication mechanisms and security misconfigurations. API Developers must **safeguard APIs in line with best cyber security practices**. The modules like sign-in, role-based access, user profile setting etc., must be given more importance as malicious actors tend to target known endpoints for gaining access to the system.
