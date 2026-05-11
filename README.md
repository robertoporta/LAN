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
<img width="895" height="527" alt="image" src="https://github.com/user-attachments/assets/ec94414e-55c1-4ab2-a4d3-12c85e797ad8" />
</p>
<br>

<p>
- For internet connections, I configure a default route toward the ISP so unknown traffic can exit the enterprise network. Next, I enable OSPF in area 0 so internal devices can dynamically learn routes. To finish R1’s configuration, I advertise the default route into OSPF so all internal networks can reach the internet.
</p>
<p>
<img width="681" height="167" alt="image" src="https://github.com/user-attachments/assets/6fb86b44-231f-4091-9495-ffb4b2f0dcc3" />
</p>
<br />

<p>
- Next up is SPINE1, where I enable Layer 3 routing so the switch can function as a routing device. Then I convert the uplink interfaces into routed ports using “no switchport” so they can carry Layer 3 traffic. The connection to R1 uses the 10.0.0.4/30 subnet, while the connections down to the leaf switches use 10.0.1.0/30 for LEAF1 and 10.0.1.4/30 for LEAF2. After that, I assign IP addresses to each interface and bring them up so communication can be established.
</p>
<p>
<img width="896" height="581" alt="image" src="https://github.com/user-attachments/assets/f7f484f4-6bf3-4df7-a391-b0b0747ce48f" />
</p>
<br />

<p>
- Lastly on SPINE1, I enable OSPF so it can participate in dynamic routing, and advertise all connected networks.
</p>
<p>
<img width="894" height="155" alt="image" src="https://github.com/user-attachments/assets/4df1b2fd-8b1b-43a8-a9f9-8a41a787eadf" />
</p>
<br>

<p>
- Onto the SPINE2 core switch, I also start by enabling Layer 3 routing so SPINE2 can operate in the routing core. Next, I configure routed interfaces toward R1 and the leaf switches. The link between SPINE2 and R1 uses the 10.0.0.8/30 subnet, while the links down to the leaf switches use 10.0.1.8/30 and 10.0.1.12/30. Lastly, I enable all interfaces so routing can begin.
</p>
<img width="893" height="580" alt="image" src="https://github.com/user-attachments/assets/91946bc8-f382-49aa-b6b9-62d1a833484a" />
</p>
<br />

<p>
To finish on SPINE2, I enable OSPF on SPINE2 so it can participate in the shared dynamic routing domain across the spine and leaf architecture.
</p>
<p>
<img width="893" height="155" alt="image" src="https://github.com/user-attachments/assets/d8e80ed5-4ed7-4419-9383-47c8315c1141" />
</p>
<br />

<p>
- This is an updated view of what the topology looks like up to this point, with added subnet labels. Being able to know all the subnets is something crucial for configuring interfaces and troubleshooting issues you might run into.
</p>
<p>
<img width="693" height="577" alt="image" src="https://github.com/user-attachments/assets/4404d8d8-d8d7-4b91-9ff3-77c31972c6dd" />
</p>
<br />

<p>
- Going down the topology, next is the configuration for the LEAF1 and LEAF2 access switches. First in LEAF1, I begin by enabling Layer 3 routing on LEAF1 so the switch can perform inter-VLAN routing and participate in dynamic routing. I then create VLAN 10 to represent the Engineering network segment. The subnet will be 192.168.10.0/24, which will be used by devices connected to LEAF1. To allow hosts in this VLAN to communicate outside their local network, I configure an SVI with IP address 192.168.10.1/24, which serves as the default gateway for all Engineering devices.
</p>
<p>
<img width="752" height="249" alt="image" src="https://github.com/user-attachments/assets/2638c531-2a60-4519-9ad3-0bf3938acbfe" />
</p>
<br>

<p>
- 
</p>
<p>

</p>
<br>

<p>
- 
</p>
<p>

</p>
<br>

<p>
- 
</p>
<p>

</p>
<br>

<p>
- 
</p>
<p>

</p>
<br>

<p>
- 
</p>
<p>

</p>
<br>

<p>
- 
</p>
<p>

</p>
<br>

<p>
- 
</p>
<p>

</p>
<br>
