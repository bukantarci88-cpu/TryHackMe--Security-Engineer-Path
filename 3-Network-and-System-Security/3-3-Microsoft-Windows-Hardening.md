# Eng 3.3. Microsoft Windows Hardening

#### **Task 1 - Introduction**

The room aims to teach basic concepts required to harden a workstation coupled with knowledge of services/software/applications that may result in hacking a computer or data breach.

#### **Task 2 - Understanding General Concepts**

**Services:** Windows Services create and manage critical functions such as network connectivity, storage, memory, sound, user credentials, and data backup and runs automatically in the background. These services are managed by the Service Control Manager panel and divided into three categories, i.e. Local, Network & System. Many applications like browsers and anti-virus software can also run their services for a seamless user experience. Type `services.msc` in the Run window to access Windows services.

![Image for Services](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/508f1714a93326335f11c9f9804582a2.png)

**Windows Registry:** The Windows registry is a unified container database that stores configurational settings, essential keys and shared preferences for Windows and third-party applications. Usually, on the installation of most applications, it uses a registry editor for storing various states of the application. For example, suppose an application (malicious or normal) wants to execute itself during the computer boot-up process; In that case, it will store its entry in the Run & Run Once key. Usually, a malicious program makes undesired changes in the registry editor and tries to abuse its program or service as part of system routine activities. It is always recommended to protect the registry editor by limiting its access to unauthorised users. Type `regedit` in the Run dialogue or taskbar search to access the registry editor.

![Image for Accessing Registry](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/f10675954519d7470106a15273aeaa7f.png)

**Event Viewer:** Event Viewer is an app that shows log details about all events occurring on your computer, including driver updates, hardware failures, changes in the operating system, invalid authentication attempts and application crash logs. Event Viewer receives notifications from different services and applications running on the computer and stores them in a centralised database. Hackers and malicious actors access Event Viewer to increase their attack surface and enhance the target system's profiling. Event categories are as below:

- Application: Records events of already installed programs.
- System: Records events of system components.
- Security: Logs events related to security and authentication etc.

We can access Event Viewer by typing `eventvwr` in the Run window. The default location for storing events is `C:\WINDOWS\system32\config\folder` in the attached VM (`MACHINE_IP`).

![Image for Accessing Event Viewer](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/3fb4825b43009e27d7217c49d2a54e77.png)

**Telemetry:** Telemetry is a data collection system used by Microsoft to enhance the user experience by preemptively identifying security and functional issues in software. An application seamlessly shares data (crash logs, application-specific) with Microsoft to improve the user experience for future releases. Telemetry functionality is achieved by Universal Telemetry Client (UTC) services available in Windows and runs through `diagtrack.dll`. Contents acquired through telemetry service are stored encrypted in a local folder `%ProgramData%\Microsoft\Diagnosis` and sent to Microsoft after 15 minutes or so. We can access `The DiagTrack` through the Services console in Windows 10.

![Image for Diagtrack](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/4798e8d5fcae725891dd0d917da72a71.png)

> What is the startup type of App Readiness service in the services panel?
> 

Manual

 

<img width="713" height="507" alt="image" src="https://github.com/user-attachments/assets/62e99288-9846-4642-8f8a-c91a91bb02af" />


> Open Registry Editor and find the key “tryhackme”. What is the default value of the key?
> 

{THM_REG_FLAG}

 

<img width="682" height="456" alt="image 1" src="https://github.com/user-attachments/assets/bf6f5573-a017-4f03-a57d-9040c4e5b00d" />


> Open the Diagnosis folder and go through the various log files. Can you find the flag?
> 

{THM_1000710}

 

<img width="502" height="613" alt="image 2" src="https://github.com/user-attachments/assets/6f81fe03-1d14-4223-aa5a-b7bc5661646d" />


#### **Task 3 - Identity & Access Management**

**Standard vs Admin Account:** Identity and access management involves employing best practices to ensure that only authenticated and authorised users can access the system. There are two types of accounts in Windows, i.e. Admin and Standard Account. Per best practice, the Admin account should only be used to carry out tasks like software installation and accessing the registry editor, service panel, etc. Routine functions like access to regular applications, including Microsoft Office, browser, etc., can be allowed to standard accounts. Go to `Control Panel > User Accounts` to create standard or administrator accounts.

![Image for Creating Account](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/9a52c8c09ea562fc4003da40cc87a229.png)

 To access accounts and select the sign-in option, go to

```
Settings > Accounts > Sign-in Options.
```

![Image for Sign-In Options](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/51fff821ccc3b7e21698a6160df4a96b.png)

**User Account Control (UAC):** User Account Control (UAC) is a feature that enforces enhanced access control and ensures that all services and applications execute in non-administrator accounts. It helps mitigate malware's impact and minimises privilege escalation by [bypassing UAC](https://tryhackme.com/room/bypassinguac). Actions requiring elevated privileges will automatically prompt for administrative user account credentials if the logged-in user does not already possess these. To access UAC, go to `Control Panel -> User Accounts` and click on `Change User Account Control Setting`.

![Image for Changing UAC](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/5e5609be5a55c30aa42a27801c5362c4.png)

Keep the notification level "**Always Notify**" in the User Account Control Settings.

**Local Policy and Group Policies Editor:** Group Policy Editor is a built-in interactive tool by Microsoft that allows to configure and implement local and group policies. We mainly use this feature when part of a network; however, we can also use it for a workstation to limit the execution of vulnerable extensions, set password policies, and other administrative settings.

**Note**: The feature is not available in Windows Home but only in the Pro and Enterprise versions.

![Image for Accessing LPE](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/e459dd6e94f893a5db56ba8c6d2ced94.png)

**Password Policies:** One primary use of a local policy editor is to ensure complex and strong passwords for user accounts. For example, we can design password policies to maximise our security:

- Passwords must contain both uppercase and lowercase characters.
- Check passwords against leaked or already hacked databases or a dictionary of compromised passwords.
- In case of 6 failed login attempts within 15 minutes, the account will remain locked for at least 1 hour.

We can access Password policies through the Local group policy editor. Go to `Security settings > Account Policies > Password policy`

![Image for Password Policies](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/e159d0daed7b8b8f217cbcd85d10c0b2.png)

**Setting A Lockout Policy:** To protect your system password from being guessed by an attacker, we can set out a lockout policy so the account will automatically lock after certain invalid attempts. To set a lockout policy, go to `Local Security Policy > Windows Settings > Account Policies > Account Lockout Policy` and configure values to lock out hackers after three invalid attempts.

![Image for Account Lockout Policy](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/b4364de2e962d48755d37d254dddf0f9.png)

> Find the name of the Administrator Account of the attached VM.
> 

Harden

 

<img width="697" height="422" alt="image 3" src="https://github.com/user-attachments/assets/3dc9d2d6-defa-419f-885d-edfaf9dd814f" />


> Go to the User Account Control Setting Panel (Control Panel > All Control Panel Items > User Accounts). What is the default level of Notification?
> 

Always Notify

 

<img width="642" height="386" alt="image 4" src="https://github.com/user-attachments/assets/b8fce659-f94a-4406-bb36-e4c003d02194" />


> How many standard accounts are created in the VM?
> 

0

 

<img width="778" height="448" alt="image 5" src="https://github.com/user-attachments/assets/26a33cc9-d4a4-494f-b5bd-a92e71b68299" />


#### **Task 4 - Network Management**

**Windows Defender Firewall:** Windows Defender Firewall is a built-in application that protects computers from malicious attacks and blocks unauthorised traffic through inbound and outbound rules or filters. As an analogy, this is equivalent to “who is coming in and going out of your home”. Malicious actors abuse Windows Firewall by bypassing existing rules. For example, if we have configured the firewall to allow incoming connections, hackers will try to manipulate the functionality by creating a remote connection to the victim's computer. We can access Windows Defender Firewall by accessing `WF.msc` in the Run dialogue.

![Accessing Firewall Software](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/0825e4e702f7d4c9e0b5c4df81878fe4.png)

Whenever possible, enable the Windows Defender Firewall default settings. For blocking all the incoming traffic, always configure the firewall with a 'default deny' rule before making an exception rule that allows more specific traffic.

**Disable unused Networking Devices:** Network devices like routers, ethernet cards, WiFI adapters etc., enable data sharing between computers. If the device is improperly configured or not being used by the owner, it is recommended to disable the interface so that threat actors cannot access them and use them for data retrieval from the victim's computer. To disable the unused Networking Devices, go to the `Control panel > System and Security Setting > System > Device Manager` and disable all the unused Networking devices.

![Disable Unused Networking Devices](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/381409d62e6ebaf2c542849dc941f58c.png)

**Disable SMB protocol:** SMB is a file-sharing protocol exploited by hackers in the wild. The protocol is primarily used for file sharing in a network; therefore, you must disable the protocol if your computer is not part of a network by issuing the [following](https://docs.microsoft.com/en-us/windows-server/storage/file-server/troubleshoot/detect-enable-and-disable-smbv1-v2-v3) command in PowerShell.

```bash
user@machine$ Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
Path          :
Online        : True
RestartNeeded : False
```

**Protecting Local Domain Name System (DNS):** The domain name system (DNS) is a naming system that translates Fully Qualified Domain Names (FQDN) into IP addresses. If the attacker places himself in the middle, he may intercept and manipulate DNS requests and point them to attacker-controlled systems since DNS replies are neither authenticated nor encrypted. The hosts file located in Windows acts like local DNS and is responsible for resolving hostnames to IP addresses. Malicious actors try to edit the file's content to reroute traffic to their command and control server. The hosts file is located at `C:\Windows\System32\Drivers\etc\hosts`.

![Accessing Local DNS](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/011d5a2f065508cd740f211aa7a478ad.png)

**Mitigating Address Resolution Protocol Attack:** The address resolution protocol resolves MAC addresses from given IP addresses saved in the workstations ARP cache. The ARP offers no authentication and accepts responses from any user in the network. An attacker can flood target systems with crafted ARP responses, which point to an attacker-controlled machine and put him in the middle of communication between the targeted hosts. You can check ARP entries using the command **`arp -a`** in the command prompt.

```bash
user@machine$ arp -a
Interface: 192.168.231.2 --- 0x5
  Internet Address      Physical Address      Type
  192.168.231.255       ff-ff-ff-ff-ff-ff     static
  224.0.0.2             01-00-5e-00-00-02     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  239.255.255.250       01-00-5e-7f-ff-fa     static
```

The table contains MAC addresses in the middle and IP addresses in the left.  If the table includes a MAC mapped to two IPs, you are probably susceptible to an ARP poisoning attack. To clear the ARP cache and prevent the attack, issue the command `arp -d`.

**Preventing Remote Access to Machine:** Remote access provides a way to connect to other computers/networks even located at a different geographical location for file sharing and remotely make changes to a workstation. Microsoft has developed a Remote Desktop Protocol (RDP) for connecting with other computers. Hackers have exploited the protocol in the past, like the famous [Blue Keep vulnerability](https://en.wikipedia.org/wiki/BlueKeep), to gain unauthorised access to the target system. We must disable remote access (if not required) by going to `settings > Remote Desktop`. Do not attempt this in VM attached to this room.

![Accessing Remote Desktop](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/340bfd9d93e9a44e2f244fc1d2d302ea.png)

> Open Windows Firewall and click on Monitoring in the left pane - which of the following profiles is active? Domain, Private, Public?
> 

Public
 
<img width="630" height="623" alt="image 6" src="https://github.com/user-attachments/assets/8c45ca99-9cad-40ec-9c6f-512151e394a6" />


> Find the IP address resolved for the website [tryhack.me](http://tryhack.me/) in the Lab Machine as per the local hosts file.
> 

 
<img width="557" height="367" alt="image 7" src="https://github.com/user-attachments/assets/cbb0e76c-fbf8-43c9-8710-70c5272459c0" />


> Open the command prompt and enter arp -a. What is the Physical address for the IP address 255.255.255.255?
> 

 
<img width="463" height="251" alt="image 8" src="https://github.com/user-attachments/assets/7c83ff90-0571-474b-86fb-9b2a89347d1d" />


#### **Task 5 - Application Management**

**Trusted Application Store:** Microsoft Store offers a complete range of applications (games, utilities) and allows downloading non-malicious files through a single click. Malicious actors bind legitimate software with trojans and viruses and upload it on the internet to infect and access the victim's computer. Therefore, downloading applications from the Microsoft Store ensures that the downloaded software is not malicious. We can access Microsoft Application Store by typing `ms-windows-store:` in the Run dialogue.

![Image for Application Store](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/55413d1781c530e53fa175b3e2fadb84.png)

**Safe App Installation:** Only allow installation of applications from the Microsoft Store on your computer. Go to `Setting > Select Apps and Features` and then select `The Microsoft Store only`.

![Safe Application](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/adf2295862b9d01aec5d967aaa9c6433.png)

**Malware Removal through Windows Defender Anti Virus:** Windows Defender Anti Virus is a complete anti-malware program capable of identifying malicious programs and taking remedial measures like quarantine. The program used to have an entire Graphical User Interface; however, Windows 10 and newer versions manage the same through Windows Security Centre. Windows Defender primarily offers four main functionalities:

- **Real-time protection** - Enables periodic scanning of the computer.
- **Browser integration** - Enables safe browsing by scanning all downloaded files, etc.
- **Application Guard** Allows complete web session sandboxing to block malicious websites or sessions to make changes in the computer.
- **Controlled Folder Access** - Protect memory areas and folders from unwanted applications.

**Microsoft Office Hardening:** Microsoft Office Suite is one of the most widely used application suites in all sectors, including financial, telecom, education, etc. Malicious actors abuse its functionality through macros, Flash applets, object linking etc., to achieve Remote Code Execution. Hardening of Microsoft Office may vary from person to person as legitimate functionality of Microsoft Office is exploited to gain access. For example, disabling macros in a University may be helpful as no one uses it; however, banks cannot disable macros as they heavily rely on complex invoices and formulas through macros.

```bash
harden@tryhackme$ office.bat (Work in Progress)
Microsoft Office Hardened Successfully.
```

**AppLocker:** AppLocker is a recently introduced feature that allows users to block specific executables, scripts, and installers from execution through a set of rules. We can easily configure them on a single PC or network through a GUI by the following method:

![Image for App Locker](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/7809f59c32041093a48fb49e3dea1891.png)

Now, we will see how to add a rule through AppLocker to block a file based on its publisher name.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/64f6885a19f1ea54250717a3af70efc0.gif)

**Browser (MS Edge):** Microsoft Edge is a built-in browser available on Windows machines based on Chromium, inline with Google Chrome and Brave. The browser often acts as an entry point to a system for further pivoting and lateral movement. It is therefore of utmost importance to block and mitigate critical attacks carried out through a browser that include ransomware, ads, unsigned application downloads and trojans.

**Protecting the Browser through Microsoft Smart Screen**

Microsoft SmartScreen helps to protect you from phishing/malware sites and software when using Microsoft Edge. It helps to make informed decisions for downloads and lets you browse safely in Microsoft Edge by:

- Displaying an alert if you are visiting any suspicious web pages.
- Vetting downloads by checking their hash, signature etc against a malicious software database.
- Protecting against phishing and malicious sites by checking visited websites against a threat intelligence database.

To turn on the Smart Screen, go to `Settings > Windows Security > App and Browser Control > Reputation-based Protection`. Scroll down and turn on the `SmartScreen option`.

![Images for Smart Screen](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/79b7490c1617095a385f943342d13176.png)

Open Microsoft Edge, go to Settings and then click “**Privacy, Search and Services**” - Set "**Tracking prevention**" to **Strict** to avoid tracking through ads, cookies etc.

![Images for Browser Control](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/b7e3bb52cc6ea640aa487f6124dcbb72.png)

**Answer the questions below**

> Windows Defender Antivirus is configured to exclude a particular extension from scanning. What is the extension?
> 

.ps


<img width="497" height="636" alt="image 9" src="https://github.com/user-attachments/assets/3f476c9e-dc24-45cd-abb2-dd7a4d98514b" />


Manage Settings > Exclusions


<img width="585" height="436" alt="image 10" src="https://github.com/user-attachments/assets/ebe20ac3-74d8-452d-a56d-2ead0de502dd" />


> A Word document is received from an unknown email address. It is best practice to open it immediately on your personal computer (yay/nay).
> 

nay

> What is the flag you received after executing the Office Hardening Batch file?
> 

{THM_1101110}


<img width="806" height="187" alt="image 12" src="https://github.com/user-attachments/assets/49aede7d-8f8d-4077-9b91-2d8bf31f4ab5" />
<img width="698" height="451" alt="image 11" src="https://github.com/user-attachments/assets/a5b4a161-9b1b-46cf-a9e8-ead2d89c0eca" />


#### **Task 6 - Storage Management**

**Data Encryption Through BitLocker:** Encryption of the computer is one of the most vital things to which we usually pay little attention. The worst nightmare is that someone gets unfettered access to your devices' data. Encryption ensures that you or someone you share the recovery key with can access the stored content. Microsoft, for its business edition of Windows, utilises the encryption tools by BitLocker. Let us have a quick look at how one can ensure to protect the data through BitLocker encryption features available on the Home Editions of Windows 10. Go to `Start > Control Panel > System and Security > BitLocker Drive Encryption`. You can easily see if the option to BitLocker Drive Encryption is enabled or not.

![Image for Bitlocker Drive Encryption](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/e36ecbbe7b00820e10c38199baa357c5.png)

A trusted Platform Module chip TPM is one of the basic requirements to support BitLocker device encryption. Keeping the BitLocker recovery key in a secure place (preferably not on the same computer) is imperative.  

**Windows Sandbox:** To run applications safely, we can use a temporary, isolated, lightweight desktop environment called Windows Sandbox. We can install software inside this safe environment, and this software will not be a part of our host machine, it will remain sandboxed. Once the Windows Sandbox is closed, everything, including files, software, and states will be deleted. We would require Virtualisation enabled on our OS to run this feature. We cannot try this in the attached VM but the steps for enabling the Sandbox feature are as below:

`Click Start > Search for 'Windows Features' and turn it on > Select Sandbox > Click OK to restart`

![Image for Sandbox](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/42ad322953f66fdd2d911f331b54a49a.png)

If you want to close the Sandbox, click the `close button,` and it will disappear. Opening suspicious files in a Windows Sandbox before blindly executing them in your base OS is recommended.

**Windows Secure Boot:** Secure boot – an advanced security standard - checks that your system is running on trusted hardware and firmware before booting, which ensures that your system boots up safely while preventing unauthorised software access from taking control of your PC, like malware. You are already in a secure boot environment if you run a modern PC with Unified Extensible Firmware Interface UEFI (the best replacement for BIOS) or Windows 10. You can check the status of the secure boot by following:

![Image for Secure Boot](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/7e86a928fcad06fc3a30d1e69620fa45.png)

The incredible thing is that you do not need to enable or install it as it works silently in the background. Windows allows you to disable these features, which is not recommended.  You can enable [Secure boot from BIOS settings (opens in new tab)](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/disabling-secure-boot?view=windows-11)(if disabled).

**Enable File Backups:** The last option, but certainly not the least important one to prevent losing irreplaceable and critical files is to enable file backups. Despite all the above techniques, if you somehow lose essential data/files, you can recover the loss by restoring it, if you have a file backup option. Creating file backups is the best option to avoid disasters like malware attacks or hardware failure. You can enable the file backup option through  `Settings > Update and Security > Backup`:-

![Image for Backup](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/c2e8a9441b14db952c6771518efd047f.png)

Therefore, the most convenient option is enabling it from the '`File History`' option - a built-in functionality of Windows 10 and 11.

**Answer the questions below**

> A security engineer has misconfigured the attached VM and stored a BitLocker recovery key in the same computer. Can you read the last six digits of the recovery key?
> 

377564

<img width="750" height="323" alt="image 13" src="https://github.com/user-attachments/assets/a4f0cb66-2c7e-4f4a-b805-0eacd238404b" />


> How many characters does the BitLocker recovery key have in the attached VM?
> 

48

> A backup file is placed on the Desktop of the attached VM. What is the extension of that file?
> 

bkf


<img width="407" height="508" alt="image 14" src="https://github.com/user-attachments/assets/71167563-f259-42e1-a746-38d0935cd26e" />


#### **Task 7 - Updating Windows**

Hackers are continuously bypassing and exploiting Windows' legitimate features. You can see a list of Windows vulnerabilities. The most critical part of hardening computers is enabling the Windows auto-updates.

`Click Start > Settings > Update & Security > Window Updates.`

This ensures that all the urgent security updates, if any, are installed immediately without causing any delay. It is most important because the quicker you apply the new Windows protection patch, the faster you can fix the potential vulnerabilities – to ensure the security from the latest known threats.

![Image for Windows Update](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/ca26fa3afcbabf99ce1d98b0396659c6.png)

Remember, users who run the older Windows versions are always at greater risk and vulnerable to new security threats. So, be very careful about this.

**Answer the questions below**

> What is the CVE score for the vulnerability CVE ID CVE-2022-32230?
> 

7.8


<img width="901" height="451" alt="image 15" src="https://github.com/user-attachments/assets/0427a577-ac8b-4194-9384-1988c118369d" />


#### **Task 8 - Cheatsheet for Hardening Windows**


<img width="1093" height="777" alt="image 16" src="https://github.com/user-attachments/assets/423f62fc-9360-47fe-b6c7-37683e9a3007" />


Level 1 - Identity & Access Management:

Actions: Create Standard & Admin accounts > Use strong passwords > Enable lock-out policies

Level 2 - Network Level: 

Actions: Turn on Windows Firewall > Disable unused network devices > Disable remote access > Protect DNS, ARP, and against MiTM

Level 3 - Application Level: 

Actions: Enable Windows Defender Antivirus > Download apps only from trusted sources > Turn on safe browsing > Enable AppLocker

Level 4 - Storage: 

Actions: Enable Bitlocker > Turn on Windows Sandbox > Set up file backups > Enable Secure Boot
