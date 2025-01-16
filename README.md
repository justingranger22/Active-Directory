
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

 Active Directory Deployed in the Cloud (Azure)</h1>
 
This tutorial explains how to setup and install Active Directory using Microsoft Virtual Machine



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1 Create Virtual Machines and Resource Group
- Step 2 Turning off the Firewall
- Step 3 Connecting the user VM to the domain controller
- Step 4 Checking to see if they connected using the ping command

<h2>Deployment and Configuration Steps</h2>

<p>
  
![image](https://github.com/user-attachments/assets/e3693d0f-fbc8-45f8-81ec-fa8c119d9eb5)
To start, create a Resource group and a VM (virtual machine). I have a more detailed example in my OS Ticket installation tutorial if you need help. You will need to set up two VM (one is the Domain Controller and the other is a user). Make sure both are set-up in the same region. The domain controller image needs to be under Windows Server and the user is Windows 10 pro otherwise this will NOT work and you will have to create a new domain controller VM. Also make sure the domain controller and user are in the same vnet that you created.
</p>
<p>

</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/c19a06c4-8171-41c2-bffc-63a7e4d17bd7)
After you got the VMs set up you have to go the domain controller networking settings and click on the network interface/ipconfig box, then on the bottom you should see ipconfig1, click on that and change the private IP address settings to static so the private IP address will not change. If you leave it on dynamic it could possibly change the IP address so make sure you click static then click save
</p>
<p>

</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/a1b8ccaa-7c91-4573-9c7a-9f64ce70794c)
Log into remote desktop with the public IP address of the domain controller. When you are logged in you should see the Server Manager screen load up to let you know that you created the right VM. If this does not show up that means you either logged in to the wrong VM or most likely you did not put the Windows Server image when you created the domain controller VM. If you at any point need to check which remote desktop you are on just go to settings and type about my PC and it will give you the information. If everything is good go ahead and right click the windows icon and click run, then type wf.msc which will bring up the Windows firewall and click properties. Turn off the first three tabs then click apply and ok.  This is only for practice and you might not have to do this at a job but its good to know if ever needed.
</p>
<p>
  
![image](https://github.com/user-attachments/assets/ea736631-74b6-4e9d-818b-10844c1660d1)
In this step you will need to back to your user VM and go to network settings like before but instead click on the DNS server tab and put the PRIVATE IP address from the domain controller to the user so that they are connected. This is the part where alot of people struggle. Just make sure that you followed everything and that both private IP addresses are not already the same otherwise you will get an error message when you try to save the DNS sever settings. Then click restart (NOT refresh) on the top and it should work.

</p>

![image](https://github.com/user-attachments/assets/6c353cfa-d91e-4919-b640-23ebe2ba32f6)
To check if the user connected successfully, log into the user account on remote desktop and type powershell in the search box, then type ping (your domain controller's private IP address) and hit enter. Your screen should look like this if done correctly otherwise you will get a message that reads Destination Host Unreachable which means it can't find the IP address and therefore will not connect. You will have to go back and fix the issue. If you want to double check type ipconfig /all and towards the bottom under DNS Servers it should show you the same IP address as your domain controller. This will ensure that you did everything correct
<br />
