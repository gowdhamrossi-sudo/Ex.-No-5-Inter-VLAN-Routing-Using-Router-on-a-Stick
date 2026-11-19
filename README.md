# Ex. No: 5 Inter-VLAN Routing Using Router-on-a-Stick
# Date:
________________________________________
# Objective
To configure Inter-VLAN routing using a single router interface with subinterfaces (Router-on-a-Stick) so that hosts in different VLANs can communicate with each other.
________________________________________
# Apparatus/Tools Required
•	Cisco Packet Tracer<br>
•	1 Router (e.g., 2911)<br>
•	1 Managed Switch (e.g., 2960)<br>
•	4 PCs<br>
•	Straight-through Ethernet cables<br>
________________________________________
# Network Topology Diagram

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/0748636c-34b7-42c7-9e9d-b8a820aa0f38" />

# Description:
•	PC0 and PC1 belong to VLAN 10 (192.168.10.0/24)<br>
•	PC2 and PC3 belong to VLAN 20 (192.168.20.0/24)<br>
•	Switch connected to Router via a trunk port (FastEthernet0/1 on switch → GigabitEthernet0/0 on router)<br>
•	Router subinterfaces handle VLAN routing<br>
(Insert screenshot of your Packet Tracer setup here)<br>
________________________________________
# IP Addressing Table
Device	VLAN	IP Address	Subnet Mask	Port/Interface<br>
PC0	10	192.168.10.1	255.255.255.0	FastEthernet0/1<br>
PC1	10	192.168.10.2	255.255.255.0	FastEthernet0/2<br>
PC2	20	192.168.20.1	255.255.255.0	FastEthernet0/3<br>
PC3	20	192.168.20.2	255.255.255.0	FastEthernet0/4<br>
Router G0/0.10	10	192.168.10.254	255.255.255.0	Subinterface VLAN 10<br>
Router G0/0.20	20	192.168.20.254	255.255.255.0	Subinterface VLAN 20<br>
________________________________________
# Procedure
1.	Setup devices in Packet Tracer: Place 4 PCs, 1 switch, and 1 router.<br>
2.	Cabling:<br>
o	PCs to switch ports (PC0–F0/1, PC1–F0/2, PC2–F0/3, PC3–F0/4)<br>
o	Switch F0/5 to Router G0/0<br>
3.	Assign IP addresses to each PC as per the IP table.<br>
4.	Switch Configuration:<br>
o	Create VLAN 10 and VLAN 20<br>
o	Assign ports F0/1–F0/2 to VLAN 10, ports F0/3–F0/4 to VLAN 20<br>
o	Configure trunk on port F0/5 to the router<br>
5.	Router Configuration (Router-on-a-Stick):<br>
o	Enable subinterfaces G0/0.10 and G0/0.20<br>
o	Assign encapsulation dot1q for each VLAN ID<br>
o	Assign IP addresses to each subinterface (default gateway for respective VLANs)<br>
6.	Testing:<br>
o	Ping from PC0 to PC2 (should succeed after routing is configured)<br>
o	Ping between PCs in the same VLAN (should succeed)<br>
________________________________________
# Commands Used
Switch Configuration:<br>
python<br>
CopyEdit<br>
Switch> enable<br>
Switch# configure terminal<br>
Switch(config)# vlan 10<br>
Switch(config-vlan)# name STAFF<br>
Switch(config-vlan)# exit<br>
Switch(config)# vlan 20<br>
Switch(config-vlan)# name STUDENTS<br>
Switch(config-vlan)# exit<br>
Switch(config)# interface range fastethernet0/1 - 2<br>
Switch(config-if-range)# switchport mode access<br>
Switch(config-if-range)# switchport access vlan 10<br>
Switch(config-if-range)# exit<br>
Switch(config)# interface range fastethernet0/3 - 4<br>
Switch(config-if-range)# switchport mode access<br>
Switch(config-if-range)# switchport access vlan 20<br>
Switch(config-if-range)# exit<br>
Switch(config)# interface fastethernet0/5<br>
Switch(config-if)# switchport mode trunk<br>
Switch(config-if)# exit<br>
Router Configuration:<br>
arduino<br>
CopyEdit<br>
Router> enable<br>
Router# configure terminal<br>
Router(config)# interface gigabitethernet0/0.10<br>
Router(config-subif)# encapsulation dot1Q 10<br>
Router(config-subif)# ip address 192.168.10.254 255.255.255.0<br>
Router(config-subif)# no shutdown<br>
Router(config)# interface gigabitethernet0/0.20<br>
Router(config-subif)# encapsulation dot1Q 20<br>
Router(config-subif)# ip address 192.168.20.254 255.255.255.0<br>
Router(config-subif)# no shutdown<br>
Router(config)# interface gigabitethernet0/0<br>
Router(config-if)# no shutdown<br>
________________________________________
# Output (Screenshots)
•	VLAN configuration on the switch<br>
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/80d9ca18-93b7-44be-bb9b-b2dd64c7ac71" />

•	Router subinterface configuration<br>
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/af13b373-0337-4de2-b5bb-336e89f90bd7" />

•	PC IP settings<br>
PC1

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/cd432dbf-c4b4-4cba-ba71-f978cd0dc549" />

PC2
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/7231a1f8-493a-4904-b747-d64edaaa0073" />

PC3
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/0737e0dd-b653-4ca0-b9e2-2a2ec2489e70" />

PC4
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/0effcc7a-a833-4b10-af5e-4b6882e4c5a9" />

•	Successful ping between PCs in different VLANs after routing<br>
<img width="1920" height="1200" alt="Screenshot (223)" src="https://github.com/user-attachments/assets/cdfab1b0-9996-4e26-8577-fd0572f7c6cc" />

•	Successful ping between PCs in the same VLAN<br>
<img width="1920" height="1200" alt="Screenshot (221)" src="https://github.com/user-attachments/assets/f7de5f12-f3b9-4b09-a1f1-0ae5efcb8213" />

________________________________________
# Result
Inter-VLAN routing was successfully configured using the Router-on-a-Stick method. PCs in different VLANs could communicate through the router.

