<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

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

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create VM1
  <ul>
    <li>First Create VM1 with image as Windows 10 pro, Size 3-2vcpus, create resource group with a name you desire.</li>
    <li>Create VM2 with image Ubunto Server (Linux), Same size and use same resource group you initially created</li>
    <ul>
    <li> Check the password box under administrator account and you can use similar login information as VM1 </li>
    <li> After clicking next to Networking make sure the Vnet is the same vnet as VM1</li>
    </ul>
  </ul>
</p>
<br />
<h3>Observe ICMP Traffic</h3>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <ul>
<li>Use Remote Desktop to connect to your Windows 10 Virtual Machine</li>
<li>Within your Windows 10 Virtual Machine, Install Wireshark</li>
<li>Open Wireshark and filter for ICMP traffic only</li>
<li>Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM</li>
<li>Observe ping requests and replies within WireShark</li>
<li>From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark</li>
<li>Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM</li>
<li>Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic</li>
<li>Create a rule: DENY_ICMP_FROM_ANYWHERE</li>
<li>Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity</li>
<li>Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using</li>
<li>Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)</li>
<li>Stop the ping activity</li>
  </ul>
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
