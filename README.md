<h1>SOHO Netwwork Project</h1>


<h2>Description</h2>
# SOHO Network Implementation

## Project Overview
This project involved designing and implementing a secure and efficient network infrastructure for a small network using VLANs, inter-VLAN routing, and DHCP...

## Network Requirements
### Devices Used:
- 1 Router (Cisco)
- 1 Switch (Cisco)
- 3 PCs (One for each department)
- 3 Printers (One for each department)
- 1 Laptop (Customer Service Department)
- 1 Smartphone (Customer Service Department)

### VLANs & Port Assignments:
- **VLAN 10 - Admin/IT:** Fa0/3, Fa0/4, Fa0/5
- **VLAN 20 - Finance/HR:** Fa0/6, Fa0/7, Fa0/8
- **VLAN 30 - Customer Service/Reception:** Fa0/9, Fa0/10, Fa0/11

### Additional Requirements:
- Devices must obtain IPv4 addresses automatically via DHCP.
- All departments should be able to communicate.
- Wireless access for customer service devices.

## Subnetting & IP Addressing
The ISP provided the base network `192.168.1.0/24`, which was subnetted as follows:
- **VLAN 10 (Admin/IT):** `192.168.1.0/26` (Usable Range: `192.168.1.1 - 192.168.1.62`)
- **VLAN 20 (Finance/HR):** `192.168.1.64/26` (Usable Range: `192.168.1.65 - 192.168.1.126`)
- **VLAN 30 (Customer Service/Consultation):** `192.168.1.128/26` (Usable Range: `192.168.1.129 - 192.168.1.190`)

## Network Configuration Steps
### 1. Creating VLANs & Assigning Ports
```bash
Switch(config)# vlan 10
Switch(config-vlan)# name Admin/IT
Switch(config-vlan)# vlan 20
Switch(config-vlan)# name Finance/HR
Switch(config-vlan)# vlan 30
Switch(config-vlan)# name CustomerService/Consultation
Switch(config-vlan)# exit
```

### 2. Configuring Inter-VLAN Routing (Router-on-a-Stick)
```bash
Router(config)# interface fa0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.1.1 255.255.255.192
Router(config-subif)# exit
```

### 3. Configuring DHCP Server on the Router (No Excluded IPs)
```bash
Router(config)# ip dhcp pool Admin-Pool
Router(dhcp-config)# network 192.168.1.0 255.255.255.192
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# exit
```

### 4. Configuring Wireless Access for Customer Service Devices
```bash
AP(config)# interface Dot11Radio0
AP(config-if)# ssid CustomerServiceWiFi
AP(config-ssid)# authentication open
AP(config-ssid)# guest-mode
AP(config-ssid)# exit
AP(config-if)# exit
```

### 5. Testing & Verifying Network Communication
```bash
PC> ipconfig
PC> ping 192.168.1.1
PC> ping 192.168.1.65
PC> ping 192.168.1.129
```

## Conclusion
This project successfully implemented a fully functional and efficient network infrastructure for SOHO Networks...

<br />


<h2>Packet Tracer Image</h2>

<p align="center">
Packet Tracer: <br/>
<img src="https://i.imgur.com/rsSTtqI.png" height="80%" width="80%" alt="soho Network"/>
<br />



<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
