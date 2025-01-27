## Simplified Guide: Wireshark Filters for Network Analysis with Practical Exercises (Master network troubleshooting with Wireshark through real-world hands-on exercises).

### What is Wireshark?
Wireshark is a network protocol analyzer, it is like a microscope for your network—it lets you capture and analyze the data (packets) traveling across it. These packets hold valuable information, helping you troubleshoot issues, monitor activity, and even spot security concerns.

However, capturing traffic on a busy network can produce overwhelming amounts of data. That’s where filters come in—they help focus on the packets that matter most.

### Why Use Filters in Wireshark?
Find Relevant Data: Focus on specific packets related to devices, protocols, or events.

Speed Up Troubleshooting: Quickly isolate problems like connectivity issues or anomalies.

Organize Your Analysis: Separate useful data from background noise.

### Wireshark Filters: Practical Exercises
### Setting Up

Provision two Azure vitual Machines, Window 11 pro version 24Hz-x64 Gen2 and Ubuntu pro 24.04 LTS-x64 Gen2

Authentication type: Username/Password 

Ensure both VMs are in the same Virtual Network / Subnet (for seemless communication between the vms)

### Prepare Your Environment:

Use Remote Desktop to connect to a Windows 11 Virtual Machine (VM).
Install Wireshark on the Windows 11 VM. (www.wireshark.org)
choose window x64 installer and follow through with the prompt and instructiions

![WireShark Insteller](https://i.imgur.com/PrtKD7S.png)

### Retrieve VM Information:

Locate the private IP address of your Ubuntu VM (from your cloud dashboard or terminal) 
From the Windows 11 VM, ping your Ubuntu VM using its private IP.

If installation is complate and start sinffing pocket of data you will see a graph at the ethenert ber

![Wireshark interface](https://i.imgur.com/J6sMU7k.png)

### Hands-On Exercises
### 1. Observe ICMP Traffic on WireShark Interface
ICMP (Internet Control Message Protocol) is used for actions like pings to check if a device is reachable.

### Filter: icmp
Steps:
In Wireshark, apply the ICMP filter.
From the Windows 11 VM, 
Observe the ping requests and replies in Wireshark.

![ICMP](https://i.imgur.com/5cb8Nec.png)

Expand the etharnet and see the MAC of bothe the source and the destination

![MAC](https://i.imgur.com/HPERApD.png)


Now ping a public website like www.google.com and observe the ICMP traffic.
Challenge:

### Configuring a Firewall [Network Security _Group]) 
Disable incoming ICMP traffic in the Network Security Group for your Ubuntu VM.
Start a continuous ping (ping -t) from the Windows 11 VM to the Ubuntu VM.
Observe how the ICMP traffic stops.

![Firewall for inbond traffic](https://i.imgur.com/duIPwbY.png)

Re-enable ICMP traffic, and watch it resume in both Wireshark and the command line.
### 2. Observe SSH Traffic

SSH (Secure Shell) is used to securely log in to remote servers.

Filter: ssh
Steps:
Apply the SSH filter in Wireshark.
From the Windows 11 VM, use SSH to connect to your Ubuntu VM using its private IP.
Enter login commands (username and password) in the SSH terminal.
Observe the SSH traffic in Wireshark as you type commands.
Exit the SSH session and see how the traffic ends.
![SSH](https://i.imgur.com/RJk6xKm.png)

### 3. Observe DHCP Traffic
DHCP (Dynamic Host Configuration Protocol) is how devices obtain IP addresses.
Filter: dhcp
Steps:
In Wireshark, apply the DHCP filter.
From the Windows 11 VM, open the command line and type:
ipconfig /renew  
Observe the DHCP packets as the VM requests a new IP address.

![DHC](https://i.imgur.com/gG8XTqp.png)

### 4. Observe DNS Traffic
DNS (Domain Name System) resolves website names to IP addresses.

Filter: dns
Steps:
Apply the DNS filter in Wireshark.
On the Windows 11 VM, use the command line to perform DNS lookups:

nslookup google.com  
nslookup disney.com  
Observe the DNS queries and responses in Wireshark.
![DNS](https://i.imgur.com/QWgPoGh.png)

### 5. Observe RDP Traffic
RDP (Remote Desktop Protocol) is used for remote access to Windows machines.
Filter: tcp.port == 3389
Steps:
Apply the RDP filter in Wireshark.
Observe the continuous traffic generated during your remote desktop session.

![tcp.port == 3389](https://i.imgur.com/CjcsPW4.png)
Discussion: Why is RDP traffic continuous? It’s because RDP constantly updates the session to reflect actions like mouse movements or screen changes.
Bonus Filters and Use Cases

### 6 Observe HTTP (Hypertext Transfer Protocol)
HTTP (Hypertext Transfer Protocol) it is the protocol used by web browsers and servers to communicate. It handles requests like when you type a website address into your browser and responses like delivering the webpage back to you.

Steps:
Apply the  tcp.port == 80 Filter 

![tcp.port == 80](https://i.imgur.com/mzGjzis.png)

### Pro Tips for Using Wireshark
Start Broad, Then Narrow Down: Begin with simple filters and refine as needed.
Combine Filters: Use operators like &&, ||, and ! to create complex filters.
Save Filters: Frequently used filters can be saved as profiles for quick access.
Test Your Filters: Always ensure filters capture the intended traffic by validating on sample data.

### Here’s what the colors mean:

Light Purple: These packets are for TCP, like when computers have a long chat, making sure every word is heard.

Light Blue: These are UDP packets, for quick messages like "Hi!" with no response needed.

Black: These packets have errors, like a broken puzzle piece that doesn’t fit.

Light Green: These packets carry HTTP traffic, which is like the web pages you visit.

Light Yellow: These are special Windows messages, such as sharing files or connecting printers.

Dark Yellow: These packets are for routing, helping messages find the right path.

Dark Gray: These are like the handshake packets—"Hello!" (SYN), "Goodbye!" (FIN), or "Got it!" (ACK)—when computers start or end their conversations.
Wireshark uses this color coding to help you quickly spot what kind of "clues" you’re looking at in the network!

### Conclusion
Wireshark’s filters are essential for efficient network troubleshooting and analysis. By practicing with real-world scenarios, like observing ICMP, SSH, DHCP, DNS, and RDP traffic, you can build practical skills that translate directly to professional environments.

Filters simplify your analysis and save time, making you a more effective IT professional. Start experimenting with these exercises to become a Wireshark pro.

### Thank for your time

