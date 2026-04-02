# Window-Server-Home-Lab
This home lab is designed to simulate a real-world enterprise IT environment using virtualization through VMware. The primary objective is to build, configure, and manage a fully functional Windows domain infrastructure from the ground up, gaining hands-on experience with core system administration concepts.

At the foundation of this lab is a virtual machine running Windows Server 2022, which will be configured as a domain controller. From there, key services such as Active Directory Domain Services (AD DS) and Active Directory Certificate Services (AD CS) will be installed and configured to manage identity, authentication, and secure communications within the network.

Throughout this lab, I will implement and manage Group Policy Objects (GPOs) to enforce organizational policies, configure system settings, and control user environments, mirroring real enterprise practices. Additionally, I will create and manage users, security groups, and computer objects within Active Directory to simulate role-based access control and organizational structure.

To complete the environment, multiple Windows 11 Enterprise virtual machines will be deployed and joined to the domain. This will allow for testing authentication, policy application, and centralized management from the domain controller.

This lab serves as a practical foundation for developing skills in:

Windows Server administration
Identity and access management
Network and domain infrastructure
Enterprise-level system configuration and troubleshooting

By the end of this project, I will have a fully operational domain environment that reflects real-world IT scenarios, preparing me for roles in system administration, infrastructure support, and cloud engineering.

# Installing Windows Server 2022 and Active Directory

After creating the virtual machine for Windows Server 2022, boot it up and begin the installation process. Create your disk partitions, create your Administrator password, and install your VMware tools if using VMware.

<img width="1220" height="880" alt="Image1" src="https://github.com/user-attachments/assets/4148dd54-4bb1-47d4-907d-d7f810f0247d" />
<img width="1225" height="883" alt="Image2" src="https://github.com/user-attachments/assets/661f6c08-bba5-444d-928d-6adeb9eb2b83" />

After the system reboots and you are back in Server Manager, proceed with installing the Active Directory Domain Services (AD DS) role:

In the top-right corner of Server Manager, click Manage → Add Roles and Features
In the wizard, select Role-based or feature-based installation, then click Next
Under Server Selection, ensure your server is selected, then click Next
On the Server Roles page, check Active Directory Domain Services
When prompted, click Add Features, then click Next
On the Features page, click Next
On the AD DS page, review the information and click Next
On the Confirmation page, click Install

Once the installation completes, you will be ready to promote the server to a Domain Controller in the next step.

<img width="1220" height="854" alt="633b35308b526a55854a9509ae06092b" src="https://github.com/user-attachments/assets/738350b6-5642-4e79-ab46-700484fe0287" />

Once the Active Directory Domain Services (AD DS) installation is complete:

Click Close to exit the installation wizard
In the top-right corner of Server Manager, click the notification flag
Select the blue link labeled “Promote this server to a domain controller”

This will launch the Active Directory Domain Services Configuration Wizard, where you will configure your domain environment in the next steps.
Which i have named my domain "mydomain.local"

<img width="1219" height="856" alt="c284a7408136df2bd2e7838b789a5968" src="https://github.com/user-attachments/assets/45eb2f51-e081-4736-ab55-bd63b9b40526" />

To begin configuring the Active Directory environment, Organizational Units (OUs) were created to establish a structured and scalable hierarchy.

Steps Performed. → Opened Server Manager
Navigated to Tools → Active Directory Users and Computers (ADUC) → Right-clicked the domain: mydomain.local →
Selected New → Organizational Unit (OU)

The following top-level OUs were created:

EUROPE, USA, ASIAN

Each regional OU contains the following sub-OUs:

Computers, Users, Servers

A dedicated “Groups” Organizational Unit (OU) was also created to centrally manage both security and distribution groups.

<img width="1023" height="776" alt="c4262c9f162d1ff4de05572ff472a418" src="https://github.com/user-attachments/assets/7dc4c1b0-e4fe-428e-ac41-0239d26dd775" />

<img width="1221" height="870" alt="818846f1520b9a098fbf925f2d8ce6ed" src="https://github.com/user-attachments/assets/dddea5ef-4885-4f16-8b04-cae8d8086104" />

Below is a diagram illustrating the key differences between Security Groups and Distribution Groups.

<img width="1536" height="1024" alt="35c002af-bd79-490e-9de6-11e6859c27a6" src="https://github.com/user-attachments/assets/410e42cb-6656-412a-bad1-df046d762f4e" />

<img width="1536" height="1024" alt="4cc35fe2-73a9-46d0-970d-625703d31b24" src="https://github.com/user-attachments/assets/c53e164a-3bde-4ece-a77f-c77b69017748" />

User accounts were created within the designated Users OU by selecting New → User in Active Directory Users and Computers. The following accounts were configured: Van Lian, Quynh Nguyen, and Admin, each with assigned initial passwords. In a production environment, users should be required to change their password upon first login, and strong password policies should be enforced to maintain security standards.

<img width="1213" height="873" alt="c6319d630c4bdd54538812e42b3a7b96" src="https://github.com/user-attachments/assets/8b3c311a-8f23-4e39-9287-a02fece864bb" />

# Group Policy Management 

In this phase of the home lab, Group Policy Objects (GPOs) are created, configured, applied, and tested to simulate real-world policy management within an Active Directory environment. The Group Policy Management Editor was installed as part of the Active Directory setup.

The diagram below illustrates the different types of Group Policy settings and highlights the distinction between Policies and Preferences.

<img width="1536" height="1024" alt="586b4e43-1016-4122-80cd-0d84c2be2813" src="https://github.com/user-attachments/assets/4250bae1-2db2-4b48-8c49-9892ad772900" />

<img width="1536" height="1024" alt="88a3da06-bd71-439c-88c1-8e821b817c40" src="https://github.com/user-attachments/assets/a8efa8b1-2e1f-4ab4-a4d9-7f47cc8aab88" />

For the first Group Policy Object (GPO), a Password Policy was created to enforce strong password requirements and enhance overall domain security. The GPO was named “Password Policy.”

<img width="1017" height="768" alt="6318405eef6e9a709e38d3c043e98ee2" src="https://github.com/user-attachments/assets/e080aa45-e3c3-4d9d-97c1-4416e1ff475d" />

Since this is a domain-level password policy, it is configured under Computer Configuration → Policies, as these settings are enforced at the system level and cannot be modified by end users. This ensures that password requirements are centrally managed and controlled by administrators.

To configure the policy, navigate to:
Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies > Password Policy

<img width="1028" height="785" alt="dc8c27aa0e2d2d553cd24edfcfe3c240" src="https://github.com/user-attachments/assets/581061e9-5394-41f0-a7d9-c4178c2b9cb3" />

The Password Policy GPO was configured with the following settings to strengthen account security:  

Minimum password length: 10 characters  
Password complexity requirements: Enabled  
Maximum password age: 90 days  
Enforce password history: 24 passwords remembered  

These settings help ensure strong password practices, reduce the risk of compromised credentials, and prevent users from reusing previous passwords.  

<img width="1016" height="774" alt="8479a293cf3122165147ed68f5307c9d" src="https://github.com/user-attachments/assets/c77e3fa8-2db2-4ad9-b3f6-9cdeab76b1fe" />

The next Group Policy Object (GPO) created restricts access to the Control Panel, preventing users from modifying system settings they are not authorized to change.  

This policy is configured under:  
User Configuration → Policies → Administrative Templates → Control Panel  

By applying this setting, administrative control is maintained while reducing the risk of unintended system changes by end users.  

<img width="1018" height="767" alt="fe691dd1b2ff83bfa59051f21f1486b4" src="https://github.com/user-attachments/assets/09ee5773-930d-4b49-bcc9-c7a27b5d25eb" />

For this lab, the setting “Prohibit access to Control Panel and PC settings” was enabled to demonstrate how user restrictions can be enforced through Group Policy. This configuration is implemented specifically for testing purposes and will be utilized in later stages of the project.

<img width="1217" height="788" alt="efd5b40e2bc8670f11b30ccc682388ce" src="https://github.com/user-attachments/assets/9be8a850-e93b-4d8e-a101-10bae1761a3d" />

An additional Group Policy Object (GPO) titled “Account Lockout Policy” was created to enhance security by mitigating brute-force login attempts. This policy is configured to lock user accounts after 5 invalid login attempts, enforce a lockout duration of 30 minutes, and reset the account lockout counter after 30 minutes.

<img width="1027" height="760" alt="f51018941b87dc019944386d14164afe" src="https://github.com/user-attachments/assets/1f381dc3-f3e9-4246-a52b-effad847ee7d" />

To prevent administrative lockout during testing, the “Restrict Control Panel” GPO was configured to exclude the Administrator account. This was done by navigating to:  

Group Policy Management → Restrict Control Panel GPO → Delegation → Advanced  

The Administrator account was explicitly set to Deny “Apply Group Policy”, ensuring the policy does not impact administrative access.  

Finally, the policy changes were applied by running the following command:  

gpupdate /force  

<img width="1016" height="770" alt="2f88fc512b576e51ab880afa078b14b8" src="https://github.com/user-attachments/assets/872fb95c-cc2d-40b7-b8a3-da972dc26e33" />


Before creating a new virtual machine and joining it to the domain for Group Policy testing, the Windows Server was properly configured to ensure stable domain operations. This included assigning the Domain Controller a static IP address and configuring the appropriate DNS settings.

To configure the network settings, navigate to Network Configuration → Change Adapter Settings, then right-click the active network adapter and select Properties. From there, open Internet Protocol Version 4 (TCP/IPv4) and change the configuration from obtaining an IP address automatically (DHCP) to using a static IP address.

The DNS settings were configured to use the loopback address (127.0.0.1) as the primary DNS and Google DNS (8.8.8.8) as the secondary DNS. This configuration ensures reliable internal name resolution for domain services while still allowing access to external network resources.

<img width="1012" height="771" alt="75320099e93ead51854f38d73808402a" src="https://github.com/user-attachments/assets/7b38da6a-df08-488c-bf1b-6f5235398a56" />

Next, return to the client machine running Windows 11 Enterprise. Before joining the domain, the DNS settings must be properly configured to ensure the system can locate the Domain Controller.  

Navigate to Network Adapter Settings → TCP/IPv4 Properties, and set the Preferred DNS server to the Domain Controller’s static IP address. The Alternate DNS server can be set to 8.8.8.8. This configuration allows the client machine to resolve domain services correctly while maintaining external network connectivity.

<img width="1007" height="804" alt="5335bf239ada104ee5d124528562206b" src="https://github.com/user-attachments/assets/bd097812-eabc-4a0a-a219-92a2ec5c3c8a" />

Connectivity to the Domain Controller was verified by successfully pinging its static IP address from the client machine, confirming proper network communication prior to joining the domain.
"nslookup mydomain.local" is also a command to verify.

<img width="1024" height="794" alt="d309ef0697d7654f24d98bc020d7a831" src="https://github.com/user-attachments/assets/b036825b-e660-47fc-a055-f3b43f9d7062" />

To join the domain, navigate to System Properties → Computer Name → Change, then select Member of Domain and enter “mydomain.local.”  
Restart to apply changes. 

<img width="1027" height="771" alt="494c33cb39033abaf41ee649eaacf7bd (1)" src="https://github.com/user-attachments/assets/0ba3d06d-565e-49ba-a463-27739452a933" />

<img width="1030" height="783" alt="ef42a678670c3030bf42a228147a6b0d" src="https://github.com/user-attachments/assets/a6adfd42-fe9d-44ae-8662-c7a6741c356e" />

To validate the domain join, log in using one of the accounts created in Active Directory. From the sign-in screen, select Other User and authenticate using the appropriate domain user credentials.  

Successful authentication was confirmed by logging in with the domain account Quynh Nguyen, verifying that the system is properly joined to the domain and that Active Directory integration is functioning as expected.

<img width="1021" height="774" alt="d4d5f7e32bf4e1b4141ef2d5c3d37483" src="https://github.com/user-attachments/assets/1d7a59d4-0391-420c-988a-13c1e82aa453" />

Next, the configured Group Policy Objects (GPOs) were implemented and tested on the Quynh Nguyen user profile. The “Restrict Control Panel” GPO was linked to the HR and Management security groups, and the Quynh Nguyen account was added to these groups to apply the policy.  

To enforce the changes, the following command was executed on the client machine:  

gpupdate /force  

The policy was successfully applied, confirming that Group Policy targeting and enforcement are functioning as expected.  

<img width="1031" height="779" alt="2506a46f1fc911168c2fc639934d3d69" src="https://github.com/user-attachments/assets/4070200b-9e4a-4536-af6f-eb2071a1f0cd" />

<img width="1018" height="770" alt="75527f085d93802cf73c28437ff62fea" src="https://github.com/user-attachments/assets/42a9fbdb-69b1-44aa-a924-5e373252c067" />

# What i have learned from this project  

Through this home lab project, I gained hands-on experience building and managing a Windows-based enterprise environment using virtualization and Active Directory. I developed a strong understanding of deploying Windows Server 2022 as a Domain Controller, structuring environments with Organizational Units (OUs), and organizing resources to reflect real-world enterprise practices.  

This project also strengthened my ability to manage identity and access within a domain environment and apply security controls using Group Policy.  

📌 Key Skills Developed  

Configured Active Directory Domain Services (AD DS) and organized resources using OUs  
Managed users, security groups, and distribution groups  
Created and enforced Group Policy Objects (GPOs) including password and account lockout policies  
Configured static IP addressing and DNS for proper domain functionality  
Joined Windows 11 clients to the domain and validated authentication  
Tested and applied policies using gpupdate /force  
Troubleshot issues related to DNS, connectivity, and GPO application  




































