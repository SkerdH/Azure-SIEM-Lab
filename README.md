<h1>Azure SIEM Lab</h1>

<h2>Description</h2>
Project Overview:

I configured Azure Sentinel (a Security Information and Event Management system) and linked it to a live virtual machine designed as a honeypot. This setup enables us to actively monitor real-time attacks, such as RDP Brute Force attempts, originating from diverse global locations. To enhance our insights, we've developed a specialized PowerShell script to retrieve geolocation details of the attackers and display them on the Azure Sentinel Map.

Key Objectives:        
The key objectives of this initiative revolve around setting up and leveraging Azure Sentinel as a robust Security Information and Event Management system. This entails establishing a live virtual machine configured as a honeypot to actively monitor and analyze real-time cyber threats, with a specific focus on RDP Brute Force attacks originating from global locations. Our primary aim is to enhance threat visibility and incident response capabilities. To achieve this, a custom PowerShell script has been developed to extract geolocation information from the attackers and present it on the Azure Sentinel Map. By fulfilling these objectives, we aim to strengthen our cybersecurity posture, proactively identify threats, and fortify our defenses against potential security breaches.
<img src="https://i.imgur.com/7fnPnqd.png"/>
<br />
<br />


<h2>Languages and Utilities Used</h2>

- <b>Azure/b>
- <b>Sentinel</b>
- <b>PowerShell</b>
<h2>Environments Used </h2>

- <b>Azure VM</b>
- <b>WINDOWS 10</b> 

<h2>Program walk-through:</h2>

<p align="center"> 
Go to the Microsoft Azure portal, and create a virtual machine. Use all default settings except firewall. For the honeypot to work the firewall needs to allow in all traffic.<br/>
<img src="https://i.imgur.com/RfLZflr.png"/>
<br />
<br />
Next go to Log Analytics Workspace, and create one in order to store the logs of the virtual machine <br/>
<img src="https://i.imgur.com/0YZDunV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next head over to the Microsoft Defender for Cloud. Click environmental settings, turn off sql server, and change data collection to all events. <br/>
<img src="https://i.imgur.com/1U6Njok.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next go back to Log Analystics Workspace, find virtual machines, and connect to the virtual machine created previously <br/>
<img src="https://i.imgur.com/i3yy0GS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next its time to setup Mircrosoft Sentinel, and connect it to the Logs created previously. Once that is setup you can now connect to the VM created earlier. to
  do this use microsoft remote desktop, and take the ip address of the vm and enter it inside. Once inside the VM open up event viewer.<br/>
<img src="https://i.imgur.com/xtNEPlv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Inside event viewer click windows logs then security. Then go inside the VM and turn off the firwall wall. Now you can ping the VM. Next open up Powershell ISE and create a new .ps1 file.
  Next paste the following powershell script- https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1 .<br/>
<img src="https://i.imgur.com/nuUwCqQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next save it and run the script. The script will go through the windows logs security and return the failed login attempts. The script uses a geolocater website to provide detailed infomration
  on where the attacks came from.<br/>
<img src="https://i.imgur.com/ODp320r.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next open Log analytics and create a table to insert the custom logs. The custom logs will be the information printed out by the script. The logs given to it will be used to train the system
  in order to identify future logs.<br/>
<img src="https://i.imgur.com/3htQmKP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Once the data is added to the Log Analytics you can create querys to search for specific events or specific attributes <br/>
<img src="https://i.imgur.com/ugtQqkj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
You can also further customize the searches in order to help train the algorithm. This will help highlight and organize the data being sent in through the script. Such custom fields may include 
  latitude, longitude, country, timestamp. <br/>
<img src="https://i.imgur.com/N7ei0Wk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now that all the logs and tracking are configured you can open up Sentinel to get some more statistics and a more visual view. Next to change up how it looks go create a new workbook  <br/>
<img src="https://i.imgur.com/DeHGVDQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
In the workbook set up a querry to now visualize the data. <br/>
<img src="https://i.imgur.com/1lHfhdh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
A visual representation as shown below displays location of where failed connectioned happened to the honeypot<br/>
<img src="https://i.imgur.com/xivhoeJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
The map after letting it run for longer <br/>
<img src="https://i.imgur.com/qMEyKua.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

