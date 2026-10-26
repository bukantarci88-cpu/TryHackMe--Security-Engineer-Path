# Eng 3.5. Network Device Hardening

#### **Task 1 - Introduction**

Network devices are the building blocks and backbone of today's contemporary and large-scale networks and systems. The role of network devices is to ensure reliable and efficient transfer, filtering, and management of data across or within networks. Many network devices range from basic layer one hubs or repeaters to layer two switches, layer three routers, load balancers, virtual private networks, and intrusion prevention systems. 

#### **Task 2 - Common Threat and Attack Vectors**

Before proceeding with our actual topic, it is imperative to understand the difference between network devices and endpoint devices. Endpoint devices refer to any device that can generate or consume data on a network, such as Laptops, Desktops, Smartphones, Tablets, Printers, Servers, and IoT Devices. They are typically located at the edge of a network and interact directly with users. 

| **Threat** | **Description** | **Attack Vector** |
| --- | --- | --- |
| **Unauthorised access** | Gain unauthorised control of a network device, and then the complete network. | • Password attacks (brute force, dictionary & hybrid)
• Exploit known vulnerabilities, e.g. RCE
• Social Engineering/Phishing attack to trick network administrators into disclosing sensitive information such as usernames and passwords of devices |
| **Denial of Service (DoS)** | Disruption of critical devices and services to make them unavailable to genuine users. | • Flooding devices with fake requests
• Exploiting vulnerabilities in logical or resource handling
• Manipulating network packets |
| **Man-in-the-Middle Attacks** | Intercept the network requests between two parties by masquerading as each other to steal sensitive information or alter/manipulate the requests. | • ARP spoofing
• DNS spoofing
• Rogue access points |
| **Privilege escalation** | Gaining higher-level privileges or rights to perform restricted actions, e.g. accessing sensitive information or executing malicious code. | • Weak passwords or use of the same passwords for user and admin accounts
• Exploiting vulnerabilities
• Misconfigurations |
| **Bandwidth theft/ hotlinking** | Linking a bandwidth-intensive resource (image or video) from an external website to its original website, without permission. This can cause increased traffic to the original website. | • Scraping large volumes of data
• DoS attacks
• Malware attacks |

**Answer the questions below**

> The device that is used to control and manage network resource is called?
> 

Network device

> A threat vector that includes disruption of critical devices and services to make them unavailable to genuine users is called?
> 

Denial of Service

#### **Task 3 - Common Hardening Techniques**

- **Updating & Patching**: Ensuring the latest version of the Operating System and underlying applications of all devices and systems and installing regular security patches is the core hardening measure. Outdated OS and applications contain vulnerabilities that attackers can exploit.
- **Disabling unnecessary services & ports**: Turn off all unnecessary services and block all ports (physical and virtual) that are not needed for system functionality. This will reduce the attack surface by minimising the number of entry points an attacker can exploit.
- **Principle of Least Privilege (POLP)**: Restrict users and processes to only the minimum necessary permissions required to perform their functions.
- **Logs Monitoring**: Implement a log monitoring system to monitor for unusual activity or security events.
- **Backup regularly**: Take routine backups of systems and configurations as they can help recover from a security incident or system failure.
- **Enforcing Strong Passwords**: Change default login passwords and use strong passwords that are at least ten characters long with a combination of small letters, capital letters, special characters, and numbers. These types of passwords protect against dictionary and brute-force attacks.
- **Multi-Factor Authentication (MFA)**: MFA is an additional security layer requiring two or more types of identification before accessing the account or system. The two factors are generally something we know (like passwords) and something we have (like biometrics).

**Importance of Secure Protocols:** They ensure that sensitive data transmitted between devices is encrypted and cannot be intercepted by malicious actors. Moreover, secure protocols also help prevent man-in-the-middle attacks and other network-based exploits. Using secure protocols, network administrators can ensure that only authorised personnel can access sensitive information and perform system administration tasks. Necessary security protocols include HTTPS, SSH, SSL/TLS, and IPsec.

**Removal/Blocking of Insecure Protocols:** In addition to using secure protocols, removing and blocking access to those insecure protocols is equally essential, which will decrease an attacker's attack surface. Most important are the protocols that transmit data in clear text without encrypting them, like FTP, HTTP, Telnet, SMTP, and more. Moreover, there are inherently secure protocols (e.g. LDAP, RDP, SIPS); however, they can allow attackers to exploit the network if configured incorrectly.

**Implementation of Monitoring and Logging Controls:** Logging in network devices is essential for detecting and investigating security incidents, identifying performance issues, and complying with regulatory requirements. It provides a record of events and activities on the device, which can be used for troubleshooting, forensic analysis, and auditing purposes. The following techniques are generally used for logging:

- **Syslog**: A protocol to standardise the transfer of log messages, with the purpose of storing and analysing log messages to a central server.
- **SNMP**: Traps a notification sent by a network device to a management system when a predefined event occurs.
- **NetFlow**: A protocol used to collect and analyse network traffic data for monitoring and security analysis.
- **Packet Captures**: Capturing network traffic and storing it for analysis using a tool like Wireshark.

**Answer the questions below**

> Suppose you are configuring a router; which of the following could be considered an insecure protocol:
> 

A: HTTPS
B: FTP *
C: SSH
D: IPsec

> The protocol for sending log messages to a centralised server for storage and analysis is called?
> 

Syslog

#### **Task 4 - Hardening Virtual Private Networks**

Virtual private networks (VPNs) are now needed in the age of remote work and online communication to protect sensitive data and preserve privacy. Yet, hardening VPNs is crucial to ensure their efficiency as cyberattacks continue to develop. Hardening VPNs entails adopting additional security measures, such as multi-factor authentication and encryption techniques, to make it more challenging for hackers to access the network. By taking these extra precautions, businesses can better safeguard their data and defend against cyberattacks, raising their security level and bringing them more peace of mind.

**Standard Hardening Practices:** Usually, all the VPN servers consist of server-side and client-side configurations through a standard config file. System administrators must understand the file's content and edit it as per best security practices.  

- The OpenVPN server config file is located at `/etc/openvpn/server/server.conf`. Once the machine is loaded, open the terminal and load the file by issuing the command `sudo nano /etc/openvpn/server/server.conf`.
- Once you made the desired changes in the file, press `Ctrl+O` and hit `Enter`, then press `Ctrl+X` to exit.
- The command `sudo systemctl restart openvpn-server@server.service` can restart the OpenVPN service.

**Moving forward, the following are some of the significant hardening practices for a VPN server:**

- **Use strong encryption algorithm:** Configure the VPN gateway to use strong encryption to protect data in transit. The **cipher** directive in the config file can be used to select the encryption scheme. The possible options for [cipher (opens in new tab)](https://community.openvpn.net/openvpn/wiki/CipherNegotiation)include AES, Blowfish, Camellia, and more. For example, **AES-128-CBC** mode means to use the AES encryption algorithm with a key size of 128-bit in Cipher Block Chaining (CBC) mode, as seen below. **AES-256-CBC** is typically considered one of the strongest cipher encryption nowadays.

```bash
thm@machine$ sudo nano /etc/openvpn/server/server.conf
local MACHINE_IP
port 1194
proto udp
dev tun
ca ca.crt
cert server.crt
key server.key
cipher AES-128-CBC #cipher options can be modified
dh dh.pem
auth SHA256 tls-crypt tc.key
topology subnet
```

- **Keep VPN gateway software up-to-date**: Ensure that the VPN gateway software is always updated with the latest security patches and updates. Every VPN software has a different method for it. You can use `sudo apt upgrade openvpn` to update OpenVPN (please note that the attached VM does not have an internet connection).
- **Implement strong authentication:** Use strong authentication mechanisms such as a combination of Transport Layer Security (TLS) and a secure hashing algorithm. We can use the `auth` directive to specify the exact algorithm in the OpenVPN configuration file to ensure that a secure hashing algorithm will be used for packet authentication. Some of the [options(opens in new tab)](https://community.openvpn.net/openvpn/wiki/Openvpn24ManPage#--auth%20alg) for auth directive are **SHA1, SHA128, SHA256, SHA512 and MD5**. You can set the auth directive through the following command:

```bash
thm@machine$ sudo nano /etc/openvpn/server/server.conf
local MACHINE_IP
port 1194
proto udp
dev tun
ca ca.crt
cert server.crt
auth SHA256 #use this to change the auth parameter
tls-crypt tc.key
topology subnet
```

- **Change default settings**: Change the default usernames and passwords to something unique to reduce the risk of unauthorised access to the VPN gateway.
- **Enable Perfect Forward Secrecy (PFS)**: Perfect Forward Secrecy (PFS) in OpenVPN generates unique session keys for each session to strengthen the security of the VPN connection. Because of this, even if a hacker successfully obtained a session key, they could not use it to decode more sessions. For each session, PFS generates a new set of encryption keys, preventing the possibility of remotely decrypting previously acquired material. As a result, it is far more challenging for an attacker to spoof the VPN connection and steal sensitive data. We can use the `tls-crypt` directive in the OpenVPN configuration file to enable PFS. The `tls-crypt` directive requires a key that can be generated using the command `sudo openvpn --genkey --secret my.key` and should be placed in the same directory on the server. Choosing the appropriate cipher and auth, like **cipher AES-256-CBC** and **auth SHA 256**, supports PFS if combined with tls-crypt. The exact configuration is mentioned below:

```bash
thm@machine$ sudo nano /etc/openvpn/server/server.conf
local MACHINE_IP
port 1194
proto udp
dev tun
ca ca.crt
cert server.crt
cipher AES-256-CBC
auth SHA256
tls-crypt my.key #use this to change the tls-crypt parameter
tls-version-min 1.2  #use this to change the TLS version
topology subnet
```

- **Dedicated Users for VPN Server:** Limit user access by creating a dedicated user account and group with restricted permissions specifically for running the OpenVPN server.

**Answer the questions below**

> Update the config file to use cipher AES-128-CBC. What is the flag value linked with the cipher directive?
> 

THM{CIPHER_UPDATED_1101} 

> Update the config file to use auth SHA512. What is the flag value linked with the auth directive?
> 

THM{AUTH_UPDATED_123}

 

<img width="656" height="512" alt="image" src="https://github.com/user-attachments/assets/3402c44f-fddb-4b5f-8f27-3fb09a4934c3" />


> As per the config file, what is the port number for the OpenVPN server?
> 

1194

#### **Task 5 - Hardening Routers, Switches & Firewalls**

Routers and switches must be hardened for the network infrastructure to be secure and reliable. Every network needs routers and switches, often the first line of defence against potential security risks and attacks. By hardening these devices, we can lower the possibility of unauthorised access, avoid data breaches, and ensure network service availability. Improved network performance, increased resilience against cyberattacks, and regulatory compliance are a few of the main advantages of hardening routers and switches. Routers and switches without enough hardening are susceptible to various attacks, including denial of service and network profiling.

 **Recommended Hardening Routers, Switches & Firewalls Techniques:**

- **Setting up the device**: While setting up any network device, it is necessary to fill in all relevant details like hostname, timezone, logging, and more. These features assist in conducting incident handling in case of a compromise. For example, logging must be enabled to log all the events with the default alert level `Debug`. Similarly, timezone and time synchronisation must be set accurately to properly correlate events with their occurrence time. You can enable and modify these settings through `System > System` and select the desired option.

![How to set up a device](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/27acc27c490c8b94858ef7ad2bad42ac.png)

- **Change default credentials**: Usually, the admin web interface is protected through a username and password, and people tend to ignore changing the default. A threat actor can access the router's admin interface and compromise the whole network using default credentials. We can change the default password in OpenWrt through `System > Administration`, enter a new password, and click the `Save` button.

![How to change password in openwrt](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/c2372f525095a6bcc018a53add0dc280.png)

- **Enable secure network protocols**: For a network device to maintain the confidentiality, integrity, and availability of network traffic, secure protocols must be enabled. Secure protocols like HTTPS, SSH, and SSL/TLS offer encrypted authentication mechanisms and communications to stop unauthorised access and eavesdropping. By enabling secure protocols on a router, you can reduce the risk of data breaches, man-in-the-middle attacks, and other security threats. You can enable SSH in OpenWrt through `System > Administration > SSH Access`, then select the interface and port number and click `Save & Apply`. Moreover, you can also add specific public SSH-Keys for passwordless login.

![How to disable or enable ssh](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/34a736adbec438bd5318fb92cdfeddd5.png)

- **Disabling unnecessary scripts**: Almost every network device executes some startup scripts to provide a better user experience to a user. For example, crontab is executed on startup to verify and execute any cron job. Threat actors try to gain persistent access on a network device by adding their malicious scripts on the startup. We can add/remove startup scripts and set the priority through `System > Startup`.

![How to add or remove startup binaries](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/96abbe862786f4312a0b56578ded64da.png)

- **Securing Wi-Fi**: If the router has Wi-Fi capabilities, securing the Wi-Fi by enabling strong encryption like WPA2/WPA3, disabling SSID broadcast, changing default passwords, and more.

**Answer the questions below**

> Update the password of the router to TryHackMe123.
> 

<img width="522" height="302" alt="image 1" src="https://github.com/user-attachments/assets/192286f7-c27c-411e-97f3-bcfebad1c372" />


> What is the default SSH port configured for OpenWrt in the attached VM?
> 

22


<img width="592" height="310" alt="image 2" src="https://github.com/user-attachments/assets/65e19f39-3a8a-4316-9b49-12efdb1a73f7" />


> Go through the General Settings option under the System tab in the attached VM. The administrator has left a special message in the Notes section. What is the flag value?.
> 

 THM{SYSTEM101}


<img width="497" height="418" alt="image 3" src="https://github.com/user-attachments/assets/c244c068-22d2-40a6-965c-13f30840bed3" />


> What is the default system log buffer size value for the OpenWrt router in the attached VM?
> 

64

<img width="531" height="318" alt="image 4" src="https://github.com/user-attachments/assets/1153f824-4eca-40b4-bedd-f8fad01b4833" />


> What is the start priority for the script uhttpd?
> 

50

<img width="906" height="672" alt="image 5" src="https://github.com/user-attachments/assets/b5ee42a2-6a84-45ea-b4f9-061977bacf6e" />


 **Task 6 - Hardening Routers, Switches & Firewalls - More Techniques**

- **Manage traffic rules**: Network devices allow you to create and implement traffic rules that accept/deny network traffic. For example, we notice that the data of users connected with our network device is being exfiltrated to a command and control server IP address. We can create a rule to block all traffic where the destination IP matches the attacker's command and control server. We can add/edit traffic rules through `Network > Firewall > Traffic Rules`, and click `Add` to create a new rule.

![how to configure traffic rules](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/49be5859e279b734eb63be67a45f7f7e.png)

- **Monitor traffic**: As a network administrator, keeping track of network traffic, like uploads and downloads of data at different intervals, is essential. For example, you have excessive data uploaded from one of the email servers to an unknown IP address. Such alerts enable you to take remedial measures and stop data pilferage timely. Usually, network devices provide real-time graphs to monitor the traffic. We can view real-time traffic statistics through `Status > Realtime Graph > Traffic`.

![How to view real-time traffic statistics](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/ba97ccd65f50e4a40033204ae8e81e4f.png)

- **Configuring port forwarding**: A firewall's port forwarding capability enables inbound traffic from the internet or other sources to be routed to a particular device or service on the internal network. The firewall can send incoming traffic to the appropriate device or service on the internal network by establishing port forwarding rules while blocking any other incoming traffic that does not comply with the rules. This feature helps host applications that need outside access, granting remote control of internal devices. Port forwarding should be used carefully because it can expose internal devices and services to potential security issues if improperly secured and configured. Threat actors could add new rules here for creating connections to external command and control servers. We can configure port forwarding through `Network > Firewall > Port Forwards`, and click the `Add` button.

![how to carry port forwarding](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/d9f216eb279699879693674eaf1e195d.png)

- **Monitoring scheduled tasks**: It is important to monitor scheduled tasks to confirm that the original scheduled tasks lists are not modified by a threat actor. To add or remove scheduled tasks, which in our case are handled by cron, navigate to `System > Scheduled Tasks`, add the new cron job, and click `Save`. You can learn how to create cron jobs [here(opens in new tab)](https://phoenixnap.com/kb/set-up-cron-job-linux).

![how to set up a cron job](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/0a9310b6c761997c1e1a2191b8f486b1.png)

- **Update firmware**: It is essential to update the firmware and installed packages on a regular basis to avoid any know/unknown attacks. We can update the firmware through `System > Software`.

![how to update firmware](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/1dfafd4df7da34ff724093f1ad436c13.png)

**Additional Techniques in an Enterprise Environment:** 

- **Configuring port security**: This includes limiting the number of MAC addresses registered on a switch port and taking particular action whenever unauthorised access is detected. Enabling port security enables an administrator that data is coming from a valid source and will be forwarded to a legitimate receiver.
- **Preventing ARP spoofing**: ARP spoofing is one of the most common vectors for launching man-in-the-middle attacks on the network. The threat can be mitigated by enabling static ARP tables and implementing MAC address filtering.
- **Preventing rogue DHCP servers**: The attacker creates a spoofed DHCP server that can be later on used for assigning IPs to clients and launching MITM attacks. Mitigation measures to prevent such attacks include configuring static DHCP binding and ensuring no unknown devices are added to a network through network mapping tools.
- **Enabling IPv6**: Unlike IPv4, IPv6 has built-in support of IPsec that can be used to secure network communication and provide confidentiality, integrity, and authenticity. Moreover, this will help in protection against MITM, eavesdropping, and tampering of packets in transit.

**Answer the questions below**

> What is the name of the rule that accepts ICMP traffic from source zone WAN and destination zone as this device?
> 

Allow-Ping

<img width="896" height="367" alt="image 6" src="https://github.com/user-attachments/assets/7c4c945a-4238-4218-a5e0-dbfd6c41b823" />


> What is the name of the rule that forwards data coming from WAN port 9001 to LAN port 9002?
> 

THM_PORT

<img width="881" height="443" alt="image 7" src="https://github.com/user-attachments/assets/44ad14b2-57c0-4cff-9ee1-26d5016e5469" />


> What is the version number for the available apk package?
> 

2.12.2-1

<img width="608" height="407" alt="image 8" src="https://github.com/user-attachments/assets/f315d319-1d0c-4e25-a693-e390e1fc7b54" />



#### **Task 7 - Important Tools for Network Monitoring**

| Tool | Usage Description |
| --- | --- |
| [**Nagios(opens in new tab)**](https://assets.nagios.com/downloads/nagioscore/docs/nagioscore/4/en/quickstart.html) | A popular open-source software for monitoring systems, networks, and infrastructure. It provides real-time monitoring and alerting for various services and applications. |
| [SolarWinds Network Performance Monitor(opens in new tab)](https://documentation.solarwinds.com/en/success_center/npm/content/npm_installation_guide.htm) | A comprehensive network monitoring tool that provides real-time visibility into network performance and availability. It includes network mapping, automated network discovery, and customisable dashboards. |
| [**PRTG(opens in new tab)**](https://www.paessler.com/manuals/prtg/installation) | An all-in-one network monitoring tool that provides comprehensive performance and availability monitoring. It includes real-time traffic analysis, custom dashboards, and customisable alerts. |
| [**Zabbix(opens in new tab)**](https://www.zabbix.com/download) | A powerful open-source network monitoring tool that provides real-time network performance and availability monitoring. It includes features such as customisable dashboards, network mapping, and alerting. |

Answer the questions below

> Are network monitoring tools capable of detecting bandwidth bottlenecks?
> 

yea
