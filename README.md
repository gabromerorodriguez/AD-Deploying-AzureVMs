<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuration of Active Directory Deployed in the Cloud (Azure) and Creation of Users</h1>
This tutorial outlines the implementation of Active Directory within Azure Virtual Machines and the creation of users while seamlessly interacting with the domain controller to authenticate users, manage resources, and enforce security policies within the network infrastructure.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Deployment and Configuration of VMs within Azure.  
- Installation of Active Directory Domain Services. 
- Adding a Computer to a Domain.
- Creation of Active Directory users using a PowerShell Script. 

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="711" alt="Capture1" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/f2c9a0e4-1ce9-4d53-98fe-7fdd7bc1b9ca">
<img width="700" alt="Capture2" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/f0177b26-64af-4042-a125-3d718a8c6c25">
</p>
<p>
Everything starts at the Azure Portal. The Azure Portal serves as the central hub for managing Azure resources. We navigated through the portal to deploy the VMs and selected the appropriate VM type (e.g., Windows Server), size (based on workload requirements), and configuration settings (e.g., disk type, OS version). During VM creation, we configured networking settings such as setting up virtual networks to ensure proper communication between VMs. As noticed, we made sure both VMs are in the same virtual network. This is crucial for the entire execution of the lab. 
</p>
<br />

<p>
<img width="222" alt="Capture3" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/00cbee5c-1618-4e99-bc66-79ab2ef1c96e">
</p>
<p>
To prevent any future connectivity issues between the VMs, we configured DC-1 IP address from dynamic to static. This stability is crucial for servers, printers, and other network devices that need to maintain consistent connections.
</p>
<br />

<p>
<img width="332" alt="Capture4" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/e76c0957-1155-49b0-b509-38010929eae2">
<img width="439" alt="Capture5" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/e58bc0ec-b7c8-47ed-b575-a4f7c84c79ca">
<img width="313" alt="Capture6" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/e97c815b-36c4-4a30-9d57-229c1f955860">
</p>
<p>
It is always a good practice to test connectivity between devices. In this case, we used the ping commmand from the Client-1 PC to DC-1 Server private IP adress but the test failed. So, inside DC-1 we configured the firewall advanced security to enable two inbound rules to accept echo requests. Then, we used the ping command again and the connection between VMs was stablished. 
</p>
<br />

<h2>Installation of Active Directory Domain Services and Promoting the Server to Domain Controller</h2>

<p>
<img width="332" alt="Capture7" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/0d2ad523-bc51-4a27-9780-7580bebeecd3">
<img width="201" alt="Capture8" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/4cddc57b-93ec-41aa-9131-81c8b08b2f78">
</p>
<p>
From the Server DC-1, we installed Active Directory Domain Services. After installation was complete, we promoted the server to domain controller. Promoting a server to a domain controller is a critical step in establishing and managing an Active Directory domain. After finishing the installation and restarting the server, we logged in to the domain controller using domain administrator credentials to verify that Active Directory services are functioning correctly. At this point, we are able to use tools like Active Directory Users and Computers to manage Active Directory objects.
</p>
<br />

<h2>Adding a Computer to a Domain</h2>

<p>
<img width="310" alt="Capture9" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/d87d1241-32a3-44a7-84cb-7e8093b05dcc">
<img width="292" alt="Capture10" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/7689954a-2fca-48ad-a69a-08fdd54fdbd9">
<img width="417" alt="Capture11" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/00bc5da9-d8f6-4cbd-95f8-b140812f9c8d">
</p>
<p>
By joining computers to the domain, users can leverage Active Directory features such as single sign-on and Group Policy enforcement. Inside the server DC-1, we created two Organizational Units, "_EMPLOYEES" and "_ADMINS." within  Active Directory Users and Computers. Then we created a new user specifying attributes such as username, password, organizational unit placement and made it member of the Domain Admins group to  hold significant administrative privileges within the domain. 
</p>
<br />

<p>
<img width="382" alt="Capture12" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/02529d1b-93fc-4149-8b15-36dd5d75bfab">
</p>
<p>
Active Directory relies heavily on DNS for service location and resource discovery. Domain-joined computers use DNS to locate domain controllers, global catalog servers, and other domain services. By using the same DNS server as the domain controller, the computer ensures efficient and reliable service location within the domain environment. Capture above shows the DNS configuration on Client-1 using DC-1 IP private adrress. 
</p>
<br />

<p>
<img width="476" alt="Capture13" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/84087573-8fad-4c71-be80-3003fde998b3">
<img width="298" alt="Capture14" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/e9450135-da4d-44a3-9159-06e3ccf95f8d">
</p>
<p>
After all configurations were made, we successfully joined Client-1 computer to the domain controller. To verify configurations, from Client-1 we used the command prompt to verify with the command "whoami" and it showed the user adlab\gabriela_admin and the command "hostname" as Client-1. 
</p>
<br />

<h2>Creation of Active Directory users using a PowerShell Script</h2>

<p>
<img width="626" alt="Capture16" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/748db65d-29e6-43a5-a4c2-a8db24ecd59a">
<img width="432" alt="Capture17" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/6e23d382-c78f-4faf-b8c5-6c3ceff7a708">
</p>
<p>
As an experiment, we used a PowerShell script to create 100 users and choose one of them to attempt to log into Client-1. 
</p>
<br />

<p>
<img width="264" alt="Capture18" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/efb95509-6d17-4f41-ac71-c9ceeca77b6a">
<img width="360" alt="Capture15" src="https://github.com/gabromerorodriguez/gabromerorodriguez-AD-Deploying-AzureVMs/assets/163021104/c5266581-40c6-4d89-b60a-cabfa11caf7a">
</p>
<p>
As noticed, we chose the user "saf.racu" and we successfully were able to log into Client-1. Note that it is very important to configure Remote Desktop for non-administrative users on Client-1 so users are able to log in. 
</p>
<br />
