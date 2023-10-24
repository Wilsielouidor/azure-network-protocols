<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Resources 
- Observe ICMP Traffic 
- Observe SSH Traffic 
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic 

<h2>Actions and Observations</h2>
<h3>Create Resources in Azure</h3>

<p><img width="1435" alt="Screen Shot 2023-10-19 at 12 52 08 PM" src="https://github.com/Wilsielouidor/azure-network-protocols/assets/142513380/800f67da-5335-4b61-a66b-f1058f5dea79">
</p>

<p>
<img width="1440" alt="Screen Shot 2023-10-19 at 12 48 56 PM" src="https://github.com/Wilsielouidor/azure-network-protocols/assets/142513380/e447a0f3-4047-4295-9b13-ae82655eadaa">
</p>

<p><img width="897" alt="Screen Shot 2023-10-19 at 12 58 54 PM" src="https://github.com/Wilsielouidor/azure-network-protocols/assets/142513380/e273e985-a84d-43af-95c9-db110223808f">
</p>

<p>
Create VM1 and VM2
  <ul>
    <li>First Create VM1 with image as Windows 10 pro, Size 3-2vcpus, create resource group with a name you desire.</li>
    <li>Create VM2 with image Ubunto Server (Linux), same size (as VM1), and resource group you initially created</li>
    <ul>
    <li> Check the password box under administrator account and you can use similar login information as VM1 </li>
    <li> After clicking next to Networking make sure the Vnet is the same vnet as VM1</li>
    </ul>
  </ul>
</p>
<br />

<h3>Observe ICMP Traffic</h3>
<p>
<img width="1440" alt="Screen Shot 2023-10-19 at 1 21 12 PM" src="https://github.com/Wilsielouidor/azure-network-protocols/assets/142513380/1a27474a-a60a-423d-957d-9465da187a71">
</p>
<p>
  <ul>
<li>Use Remote Desktop to connect to your Windows 10 Virtual Machine</li>
<li>Within Windows 10 Virtual Machine 1, Install Wireshark</li>

  </ul>
</p>
<br />

<p>
<img width="1440" alt="Screen Shot 2023-10-19 at 1 29 57 PM" src="https://github.com/Wilsielouidor/azure-network-protocols/assets/142513380/5e0ac6e8-bcc3-42ca-a51b-19853e5a15f4">

</p>
<p>
  <ul>
<li>Open Wireshark-> Click Ethernet and then the Wireshark icon to get started</li>
<li> Filter ICMP traffic by typing "icmp"</li> 
</ul>
</p>
<br />

<p>
<img width="1440" alt="Screen Shot 2023-10-19 at 1 32 44 PM" src="https://github.com/Wilsielouidor/azure-network-protocols/assets/142513380/aede8580-45dc-44eb-bae5-7afd446bda2d">
</p>
<p>
  <ul>
<li>Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM</li>
<li> Open Command line or Powershell and type in ping Private IP adress of VM2
<li>Observe ping requests and replies within WireShark</li>
<li>From The Windows 10 VM, attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark</li>
  
  </ul>
</p>
<br />

<p>
<img width="1438" alt="Screen Shot 2023-10-19 at 1 41 57 PM" src="https://github.com/Wilsielouidor/azure-network-protocols/assets/142513380/9d1d60ae-ed40-441a-bb8c-d10f69722f27">
</p>

<p><img width="1440" alt="Screen Shot 2023-10-19 at 2 10 58 PM" src="https://github.com/Wilsielouidor/azure-network-protocols/assets/142513380/a5910c6f-b728-4ace-a354-96204e7211e7">
</p>
<p>
  <ul>
  <li>Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM</li>
    <li> Go to Microsoft Azure type in Network security groups</li> 
<li>Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic by creating an inbound rule</li>
    <ul>
      <li>Click Inbound Security rules-> Click Add and a window will pop up on the side</li>
      <li> Check ICMP</li>
      <li> You can leave priority as is or put it as 200</li>
      <li>Type in : DENY_ICMP_FROM_ANYWHERE</li>
      <li> Click Add</li>
    </ul>
  </ul>
</p>
<br />

<p>
<img width="1440" alt="Screen Shot 2023-10-19 at 2 15 41 PM" src="https://github.com/Wilsielouidor/azure-network-protocols/assets/142513380/dad81c44-2372-40f4-8c2a-ea2041113d82">
</p>
<p>
  <ul>
<li>Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity</li>
<li>Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using</li>
<li>Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)</li>
<li>Stop the ping activity by typing Control C within the command line and then clear data</li>
  </ul>
</p>
<br />

<h3>Observe SSH Traffic</h3>

<p>
<img width="1440" alt="Screen Shot 2023-10-19 at 8 31 49 PM" src="https://github.com/Wilsielouidor/azure-network-protocols/assets/142513380/893343ae-4d74-4c03-86fb-5ea48f56ea11">
</p>


<p><img width="1440" alt="Screen Shot 2023-10-19 at 8 32 41 PM" src="https://github.com/Wilsielouidor/azure-network-protocols/assets/142513380/23e2a6ac-8714-4bf5-8dab-204b7df9779b">
</p>
<br />

<p><img width="1440" alt="Screen Shot 2023-10-19 at 9 10 49 PM" src="https://github.com/Wilsielouidor/azure-network-protocols/assets/142513380/c088a669-e984-4070-847b-fbe6f8a9264b">
</p>
<p>
  <ul>
<li>Back in Wireshark, filter for SSH traffic only</li>
<li>From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)</li>
  <ul>
    <li>In the powershell command line type in ssh username@private ip adress of Ubuntu Virtual Machine 2->press enter</li>
    <li> Example: ssh wlabuser@10.0.0.5</li>
    <li>Type in yes for fingerprint to put in password next</li>
    <li> Warning! When typing in the password you won't be able to see what you type just continue without making any mistakes</li>
  </ul>
<li>Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark</li>
<li>Exit the SSH connection by typing ‘exit’ and pressing [Enter]</li>
  </ul>

</p>
<br />
<h3>Observe DHCP Traffic </h3>
<p>
<img width="1038" alt="Screen Shot 2023-10-19 at 9 15 04 PM" src="https://github.com/Wilsielouidor/azure-network-protocols/assets/142513380/b2627523-d223-49e4-b776-faed6c809719">
</p>
<p>
  <ul>
<li>Back in Wireshark, filter for DHCP traffic only</li>
<li>From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)</li>
<li>Observe the DHCP traffic appearing in WireShark</li> 
  </ul>
</p>
<br />
<h3>Observe DNS Traffic</h3>
<p>
<img width="1372" alt="Screen Shot 2023-10-19 at 9 18 11 PM" src="https://github.com/Wilsielouidor/azure-network-protocols/assets/142513380/bdd8578b-b79a-4cf4-bce3-31865a3491d3">
</p>
<p>
<ul>
  <li>Back in Wireshark, filter for DNS traffic only</li>
<li>From your Windows 10 VM within a command line, use nslookup to see what google.com, instagram.com, and disney.com’s IP addresses are</li>
<li>Observe the DNS traffic being shown in WireShark</li>
</ul>
</p>
<br />

<h3> Observe RDP Traffic</h3>
<p>
<img width="1440" alt="Screen Shot 2023-10-19 at 9 19 14 PM" src="https://github.com/Wilsielouidor/azure-network-protocols/assets/142513380/99a9f09b-b5be-4804-a455-a3f96bd282da">
</p>
<p>
  <ul>
<li>Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)</li>
<li>Observe the immediate non-stop spam of traffic</li>
  </ul>
</p>
<br />


