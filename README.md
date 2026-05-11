# <p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>Spine-Leaf Campus LAN with VLAN Segmentation, Inter-VLAN Routing, EtherChannel, and Upstream Routing</h1>
This lab builds and configures a full leaf–spine Layer 3 network topology with dual spine switches, dual leaf switches, VLAN segmentation, and OSPF dynamic routing for end-to-end connectivity. The spine switches act as the core, while the leaf switches provide access-layer connectivity for end devices.
All links use /30 subnets, and OSPF advertises only directly connected networks for precise routing. Redundant uplinks ensure high availability. An ISP router simulates internet connectivity using a loopback address (8.8.8.8), allowing verification of external reachability from within the network. The following image shows what the topology looks like after the initial cable connections, pre-configuration.
</p>

<p>
<img width="564" height="470" alt="image" src="https://github.com/user-attachments/assets/ea0bf4f2-a0bc-48b2-ad4b-36cc4b27e98f" />
</p>

<h2>Technologies Used</h2>

-VLANs (802.1Q segmentation)

-Inter-VLAN Routing (SVIs on Layer 3 switch)

-EtherChannel (LACP)

-Trunking (802.1Q)

-Static Routing

-Layer 3 Switching

-Default Routing


<h2>Ticket Workflow and Resolution Process</h2>

<p>
- First, I configure and enable the interface toward the ISP using the subnet 10.0.0.0/30 so I can connect the enterprise network to the simulated internet. The ISP router is using 10.0.0.2 for its interface.
Next, I configure and enable two additional interfaces toward SPINE1 and SPINE2 using separate /30 subnets so I can provide redundant upstream routing paths. The subnet between R1 and SPINE1 will be 10.0.0.4/30 and the subnet between R1 and SPINE2 will be 10.0.0.8/30.
</p>
<p>
<img width="1126" height="802" alt="Image" src="https://github.com/user-attachments/assets/2789f98a-94af-4701-85ea-82d33a1bb949" />
</p>
<br>

<p>
- For internet connections, I configure a default route toward the ISP so unknown traffic can exit the enterprise network. Next, I enable OSPF in area 0 so internal devices can dynamically learn routes. To finish R1’s configuration, I advertise the default route into OSPF so all internal networks can reach the internet.
</p>
<p>
<img width="1127" height="803" alt="Image" src="https://github.com/user-attachments/assets/0aee868f-c73f-4992-a5a0-c7631301b60f" />
</p>
<br />

<p>
- For internet connections, I configure a default route toward the ISP so unknown traffic can exit the enterprise network. Next, I enable OSPF in area 0 so internal devices can dynamically learn routes. To finish R1’s configuration, I advertise the default route into OSPF so all internal networks can reach the internet.
</p>
<p>
<img width="681" height="167" alt="image" src="https://github.com/user-attachments/assets/6fb86b44-231f-4091-9495-ffb4b2f0dcc3" />
</p>
<br />

<p>
<img width="1126" height="802" alt="Image" src="https://github.com/user-attachments/assets/7dcc89c5-ee42-4c24-9be6-22a6b166e299" />
</p>
<p>
- After making these changes, I reply to the user with basic questions to gather more information. Collecting clear details early helps prevent unnecessary delays and allows me to better diagnose the root cause of the issue.
</p>
<br />

<p>
<img width="1128" height="802" alt="Image" src="https://github.com/user-attachments/assets/fd8f7fc5-c0f0-4e04-9704-f5896b1d6f60" />
</p>
<p>
- When the user replies, I follow up by giving them steps that can potentially help resolve the issue. This collaborative approach helps users learn small troubleshooting steps while allowing me to confirm whether the problem is software, hardware, or configuration related.
</p>

<br />
<img width="1128" height="803" alt="Image" src="https://github.com/user-attachments/assets/d9596381-fd7b-4796-ac40-7b63e88cf19b" />
</p>
<p>
- After identifying the issue and confirming that the user is fine with keeping the system as is, the ticket comes to an end. I make sure the user’s request has been fully addressed and that they are satisfied with the outcome.
</p>
<br />

<p>
<img width="1124" height="803" alt="Image" src="https://github.com/user-attachments/assets/379753ec-ffc5-4f94-b913-077550c5b7ff" />
</p>
<p>
- Finally, I change the ticket status to “Resolved” and close it. Properly closing tickets keeps the help desk system organized, ensures performance metrics stay accurate, and confirms that the issue has been officially completed.
</p>
<br />

<br>
