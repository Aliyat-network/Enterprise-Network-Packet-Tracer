# Enterprise Network Design & Implementation Using Cisco Packet Trace
This project demonstrates the design and implementation of a small enterprise network using Cisco Packet Tracer.
The network consists of two locations:
- Headquarters (HQ)
- Branch Office
Each location contains three departments:
- Human Resources (HR)
- Sales
- Finance

The network was designed to provide departmental segmentation, automatic IP address allocation, inter-VLAN communication, and dynamic routing between the two locations.
🏢 Network Architecture
#Headquarters
- HR Department
- Sales Department
- Finance Department

#Branch Office
- HR Department
- Sales Department
- Finance Department

The two locations are connected through a WAN link using two Cisco routers.
The main objectives of this project are to:
- Design an enterprise network topology
- Implement VLAN segmentation
- Configure IPv4 addressing
- Configure DHCP
- Implement Inter-VLAN Routing
- Configure OSPF dynamic routing
- Test and troubleshoot network connectivity

#🛠️ Technologies & Tools

- Cisco Packet Tracer
- Cisco Routers
- Cisco Catalyst Switches
- IPv4
- VLAN
- Trunking
- DHCP
- OSPF
- Ping


# 🌐 Network Topology

<img width="960" height="504" alt="Image" src="https://github.com/user-attachments/assets/8fe47c8e-f9b1-42ac-bc5f-dbfa4f177982" />

The topology contains two enterprise locations connected through a WAN connection.

# 🔢 VLAN Configuration

<img width="443" height="505" alt="Image" src="https://github.com/user-attachments/assets/0aa31da0-62e9-490b-9f08-e82860542468" />

| VLAN | Department |
|------|------------|
| VLAN 10 | HR |
| VLAN 20 | Sales |
| VLAN 30 | Finance |
| VLAN 99 | Management |

VLANs were implemented to logically separate departments and reduce unnecessary broadcast traffic.

# IP Addressing Scheme
Headquarters(HQ)

| Department | Network | Default Gateway |
|------------|---------|-----------------|
| HR | 10.10.10.0/24 | 10.10.10.1 |
| Sales | 10.10.20.0/24 | 10.10.20.1 |
| Finance | 10.10.30.0/24 | 10.10.30.1 |

## Branch Office
| Department | Network | Default Gateway |
|------------|---------|-----------------|
| HR | 10.10.10.0/24 | 192.168.40.1 |
| Sales | 10.10.20.0/24 | 10.10.20.1 |
| Finance | 10.10.30.0/24 | 10.10.30.1 |

## WAN
| Device | IP Address |
|--------|------------|
| R1 | 10.1.100.1/30 |
| R2 | 10.1.100.2/30 |

# ⚙️ Network Configuration
1. VLAN Configuration
VLANs were created on the switches to separate the HR, Sales, and Finance departments.

Example:
cisco
vlan 10
name HR
vlan 20
name SALES
vlan 30
name FINANCE

2. Trunking
Trunk links were configured between the router and switches and between the distribution and departmental switches.
Example:
interface gigabitEthernet 0/1
switchport mode trunk
switchport trunk native vlan 30

DHCP

Cisco routers were configured as DHCP servers.

Example:

ip dhcp pool HQ-HR
network 10.10.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 8.8.8.8

This allows client PCs to automatically receive:
IP address
Subnet mask
Default gateway
DNS server

OSPF Configuration
OSPF was configured between R1 and R2 to provide dynamic routing between Headquarters and the Branch Office.
R1
router ospf 1
router-id 1.1.1.1
network 10.0.0.0 0.0.0.3 area 0
network 192.168.10.0 0.0.0.255 area 0
network 192.168.20.0 0.0.0.255 area 0
network 192.168.30.0 0.0.0.255 area 0

R2
router ospf 1
router-id 2.2.2.2
network 10.0.0.0 0.0.0.3 area 0
network 192.168.40.0 0.0.0.255 area 0
network 192.168.50.0 0.0.0.255 area 0
network 192.168.60.0 0.0.0.255 area 0

Testing & Verification
The following commands were used to verify the network.
VLAN Verification
show vlan brief

Trunk Verification
show interfaces trunk

DHCP Verification
show ip dhcp binding

OSPF Verification
show ip ospf neighbor

Routing Table
show ip route

Connectivity Testing
ping

<img width="443" height="505" alt="Image" src="https://github.com/user-attachments/assets/65e47c9e-53dc-4661-8f9f-3ae7732a58db" />

<img width="443" height="505" alt="Image" src="https://github.com/user-attachments/assets/fa446149-fcf1-49c6-9f4a-2420d46c2987" />

<img width="443" height="505" alt="Image" src="https://github.com/user-attachments/assets/75110a8b-eb3d-41e5-a3e3-b94abc606a53" />

<img width="443" height="505" alt="Image" src="https://github.com/user-attachments/assets/76fd9a0f-6440-4947-b2a5-9591d5965e67" />
