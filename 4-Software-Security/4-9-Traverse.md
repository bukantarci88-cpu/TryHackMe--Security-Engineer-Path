# Eng 4.9. Traverse

**Traverse**

Bob is a security engineer at a firm and works closely with the software/DevOps team to develop a tourism web application. Once the website was moved from QA to Production, the team noticed that the website was getting hacked daily and wanted to know the exact reason. Bob consulted the blue team as well but has yet to be successful. Therefore, he finally enrolled in the [**Software Security**](https://tryhackme.com/module/software-security) pathway at THM to learn if he was doing something wrong. Deploy the machine by clicking the `Start Lab Machine` button on the top right. You can access the website by visiting the URL `http://MACHINE_IP` via your VPN connection or the AttackBox.

Can you help Bob find the vulnerabilities and restore the website?

**Answer the questions below**

> What type of encoding is used by the hackers to obfuscate the JavaScript file?
> 

hex (First, go to the page source and click the link provided in it.)


<img width="696" height="130" alt="image" src="https://github.com/user-attachments/assets/d7deea5a-7e82-4ef0-aa87-e25326bc23ea" />


> What is the flag value after deobfuscating the file?
> 

DIRECTORY LISTING IS THE ONLY WAY

<img width="1366" height="472" alt="image 1" src="https://github.com/user-attachments/assets/699aac1a-cfe2-45f6-a7e0-e85083f9ddf2" />


> Logging is an important aspect. What is the name of the file containing email dumps?
> 

email_dump.txt

<img width="517" height="257" alt="image 3" src="https://github.com/user-attachments/assets/d577630a-fdb8-4174-abf8-4057638940d7" />
<img width="867" height="467" alt="image 2" src="https://github.com/user-attachments/assets/dd865034-864c-4d29-8c25-0ffa2be25788" />


> The logs folder contains email logs and has a message for the software team lead. What is the name of the directory that Bob has created?
> 

planning (aquasec.com SDLC)

<img width="1050" height="832" alt="image 6" src="https://github.com/user-attachments/assets/4ec23469-336b-4aba-bc8f-e87fa9467baa" />
<img width="1062" height="556" alt="image 5" src="https://github.com/user-attachments/assets/200d44ee-35d0-4311-961f-60681f111ba6" />
<img width="1268" height="327" alt="image 4" src="https://github.com/user-attachments/assets/aa9608fd-c079-4638-88d9-95b3514e19c7" />


> What is the key file for opening the directory that Bob has created for Mark?
> 

THM{100100111}

<img width="947" height="285" alt="image 7" src="https://github.com/user-attachments/assets/21148e49-ff83-4f2c-8d4e-d60248b1223a" />


> What is the email address for ID 5 using the leaked API endpoint?
> 

[john@traverse.com](mailto:john@traverse.com)


<img width="546" height="301" alt="image 8" src="https://github.com/user-attachments/assets/0e0bad5d-48e3-4c60-a53a-4dabde7f4155" />


> What is the ID for the user with admin privileges?
> 

3 


<img width="530" height="317" alt="image 9" src="https://github.com/user-attachments/assets/96f2d56d-67b2-4462-ba65-a16d2ebe9b2c" />


> What is the endpoint for logging in as the **admin**?
> 

Mention the last endpoint instead of the URL. For example, if the answer is URL is tryhackme.com/admin - Just write **/admin**. realadmin 

> The attacker uploaded a web shell and renamed a file used for managing the server. Can you find the name of the web shell that the attacker has uploaded?
> 

thm_shell.php

<img width="1042" height="692" alt="image 10" src="https://github.com/user-attachments/assets/d5262b8b-5905-4085-bf1a-e50f26060bcf" />


 write ls in whoami then execute

<img width="1070" height="866" alt="image 11" src="https://github.com/user-attachments/assets/f3000166-9c94-40be-811b-49fe9697cd83" />


> What is the name of the file renamed by the attacker for managing the web server?
> 

renamed_file_manager.php

> Can you use the file manager to restore the original website by removing the "**FINALLY HACKED**" message? What is the flag value after restoring the main website?
> 

<img width="1067" height="590" alt="image 14" src="https://github.com/user-attachments/assets/4cf0e87c-2073-4c3a-8320-5decde7c601d" />
<img width="1057" height="836" alt="image 13" src="https://github.com/user-attachments/assets/459e3a9a-a2d8-4e73-aaf6-b0db1f030357" />
<img width="992" height="820" alt="image 12" src="https://github.com/user-attachments/assets/2b8b423c-7590-41ff-87be-7adeb26f1ab5" />


---

---

---
