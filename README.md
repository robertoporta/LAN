# <p align="center">
<h1>Spine-Leaf Campus LAN with VLAN Segmentation, Inter-VLAN Routing, and Upstream Routing</h1>
This lab builds and configures a full leaf–spine Layer 3 network topology with dual spine switches, dual leaf switches, VLAN segmentation, and OSPF dynamic routing for end-to-end connectivity. The spine switches act as the core, while the leaf switches provide access-layer connectivity for end devices.
All links use /30 subnets, and OSPF advertises only directly connected networks for precise routing. Redundant uplinks ensure high availability. An ISP router simulates internet connectivity using a loopback address (8.8.8.8), allowing verification of external reachability from within the network. The following image shows what the topology looks like after the initial cable connections, pre-configuration.
</p>

<p>
<img width="564" height="470" alt="image" src="https://github.com/user-attachments/assets/ea0bf4f2-a0bc-48b2-ad4b-36cc4b27e98f" />
</p>

<h2>Technologies Used</h2>

-VLANs (802.1Q segmentation)

-Inter-VLAN Routing (SVIs on Layer 3 switch)

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
- Next, I configure both uplink interfaces as routed ports, allowing them to operate at Layer 3 and form point-to-point connections with the spine switches. Each uplink is placed into its own /30 subnet. The link between LEAF1 G0/1 and SPINE1 G0/2 uses the subnet 10.0.1.0/30, where LEAF1 is assigned 10.0.1.2 and SPINE1 uses 10.0.1.1. The second uplink between LEAF1 G0/2 and SPINE2 G0/2 uses the subnet 10.0.1.8/30, where LEAF1 is assigned 10.0.1.10 and SPINE2 uses 10.0.1.9. These point-to-point networks allow OSPF to form adjacencies with both spine switches, providing redundant upstream paths.
</p>
<p>
<img width="893" height="357" alt="image" src="https://github.com/user-attachments/assets/e72222d4-3c9c-48b7-85a8-8283e686935a" />
</p>
<br>

<p>
- With Layer 3 connectivity established, I finish LEAF1 by enabling OSPF so it can exchange routing information with the spine switches. The uplink subnets 10.0.1.0/30 and 10.0.1.8/30 are advertised to form neighbor relationships, and the VLAN subnet 192.168.10.0/24 is also advertised so it becomes reachable throughout the entire topology, allowing end devices to communicate across the network and toward the internet.
</p>
<p>
<img width="895" height="398" alt="image" src="https://github.com/user-attachments/assets/3617d2a0-4b08-49c8-860c-5cbb8fad131b" />
</p>
<br>

<p>
- The last networking device to configure is the LEAF2 access switch, I start by repeating the same Layer 3 setup but for the other department. I create VLAN 20 for the Operations department, using the 192.168.20.0/24 subnet with a default gateway of 192.168.20.1. Lastly, I configure the SVI so it acts as the Layer 3 gateway for hosts in this VLAN.
</p>
<p>
<img width="749" height="249" alt="image" src="https://github.com/user-attachments/assets/67d3429c-5be2-462b-9095-b27bda5cd14d" />
</p>
<br>

<p>
- I then configure both uplinks as routed ports to connect LEAF2 to the spine switches, connecting it upward to both spine switches using two separate point-to-point /30 networks. The link to SPINE1 uses the 10.0.1.4/30 subnet, and the link to SPINE2 uses the 10.0.1.8/30 subnet. Each interface is configured as a routed port with an IP address assigned for OSPF adjacency.
</p>
<p>
<img width="893" height="358" alt="image" src="https://github.com/user-attachments/assets/213abf1c-eb7f-437f-8208-076611903fb1" />
</p>
<br>

<p>
- Finally, I enable OSPF on LEAF2 so it can participate in dynamic routing. The uplink subnets 10.0.1.4/30 and 10.0.1.12/30 are advertised to establish neighbor relationships with the spine switches, and the VLAN subnet 192.168.20.0/24 is included so devices in the Operations network can communicate with other VLANs and reach external destinations through the routed infrastructure.
</p>
<p>
<img width="893" height="382" alt="image" src="https://github.com/user-attachments/assets/07d5c62d-9d22-4f9a-bf77-2a86a14430bc" />
</p>
<br>

<p>
- Before going onto the PC configurations, the following show commands display the routing table of all the devices, showing full OSPF connectivity across the topology. Looking at the different routes the devices have, certain routes (like the default route in the access switches, and the VLAN routes in the core router) have more than 1 available path to take. This allows for redundancy in case the principal route fails or becomes unavailable.
</p>
<p>
<img width="893" height="589" alt="image" src="https://github.com/user-attachments/assets/db0e4940-2da8-4cc5-883b-a6bb8c958f19" />
</p>
<p>
<img width="896" height="482" alt="image" src="https://github.com/user-attachments/assets/8784f531-2e2a-49fc-a7fc-c14da0d95fde" />
</p>
<p>
<img width="894" height="481" alt="image" src="https://github.com/user-attachments/assets/7d31d75d-d9e2-405d-a6ae-e514a0fa8b73" />
</p>
<p>
<img width="893" height="545" alt="image" src="https://github.com/user-attachments/assets/e840c4a4-63c1-415e-a5f4-6252532cce3b" />
</p>
<p>
<img width="894" height="549" alt="image" src="https://github.com/user-attachments/assets/97903d76-4080-4f83-ac8e-8560fd4dd530" />
</p>
<br>

<p>
- On all the PCs, I assign IP addresses based on VLAN membership and configure default gateways matching each SVI so traffic can exit correctly. The default gateway is using the first usable IP of the subnets, so the PCs will be using the following 2 usable IP addresses of each subnet.
</p>
<p>
<img width="893" height="227" alt="image" src="https://github.com/user-attachments/assets/745c8f24-7929-4308-8e71-b7eb5c675f17" />
</p>
<p>
<img width="898" height="226" alt="image" src="https://github.com/user-attachments/assets/3eff53fc-30ad-4cdc-8c17-43fb1cc90558" />
</p>
<p>
<img width="895" height="228" alt="image" src="https://github.com/user-attachments/assets/34f0995e-2b22-4ace-91b1-b8cd20739be5" />
</p>
<p>
<img width="896" height="227" alt="image" src="https://github.com/user-attachments/assets/5cd89c7c-5914-4823-9910-7cf0feae7332" />
</p>
<br>

<p>
- On PC1 from the Engineering VLAN, a test ping to the simulated internet address of 8.8.8.8, the connection is successful. Using the “tracert” command I’m able to track all the hops taken in the communication, this can be a very useful troubleshooting and verification tool. I also ran an additional ping test ping to a PC in the Operations VLAN, which was successful as well. 
</p>
<p>
<img width="857" height="335" alt="image" src="https://github.com/user-attachments/assets/c5429dda-ffef-406c-b783-b541ca6e4830" />
</p>
<p>
<img width="896" height="226" alt="image" src="https://github.com/user-attachments/assets/7c4bd71c-1b28-43e2-8d8c-452cda1d6639" />
</p>
<p>
<img width="894" height="402" alt="image" src="https://github.com/user-attachments/assets/4f9539f5-39d7-4635-9cee-49883f4bd9c5" />
</p>
<br>

<p>
- To finish the lab, on PC 4 from the Operations VLAN, I do a test ping to 8.8.8.8 and run the tracert command, showing the regular path the packet takes from LEAF2 is up to SPINE2’s G0/2 (10.0.1.9).
</p>
<p>
<img width="772" height="662" alt="image" src="https://github.com/user-attachments/assets/5f52c017-f0b3-42ec-ba2c-61b09bbecfa1" />
</p>
<br>

<p>
- Finally, I manually disabled SPINE2’s G0/2 interface to simulate a failure. I run the command again, and the ping is still successful. The tracert command shows that this time the packet went from LEAF2 to SPINE1’s FA/1 interface (10.0.1.5). This redundancy helps the uptime of a network, with connection to the internet still happening even if failure occurs.
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
