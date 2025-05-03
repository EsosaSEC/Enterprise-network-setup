# Enterprise Network Setup with VLANs, DHCP, and Inter-VLAN Routing

**Author:** Esosa Okonedo  
**Platform:** Cisco Packet Tracer  
**Date Completed:** April 2025  

## Overview

This project demonstrates the design and implementation of a scalable, segmented enterprise network in Cisco Packet Tracer. The network features VLAN-based departmental segmentation, DHCP for dynamic IP assignment, and inter-VLAN routing using a router-on-a-stick configuration for Sales and Servers, with dedicated interfaces for HR and IT.

## Network Design

| Department | VLAN ID | Subnet           | Switch Connection   |
|------------|---------|------------------|---------------------|
| HR         | 10      | 192.168.10.0/24  | Access (Gig0/0)     |
| IT         | 20      | 192.168.20.0/24  | Access (Gig0/1)     |
| Sales      | 30      | 192.168.30.0/24  | Trunk (Gig0/2.30)   |
| Servers    | 99      | 192.168.99.0/24  | Trunk (Gig0/2.99)   |

### Key Devices
- **Router**: Cisco ISR4331 (handles DHCP and inter-VLAN routing)
- **Switches**: 3 Cisco 2960 switches:
  - 1 for HR (access port to router)
  - 1 for IT (access port to router)
  - 1 shared by Sales and Servers (trunk port to router)
- **End Devices**: 2 PCs + 1 laptop per department; servers in VLAN 99

## Features Implemented

- **VLAN Segmentation**: Logical separation of HR, IT, Sales, and Servers
- **DHCP Configuration**: Dynamic IP assignment with reserved ranges (e.g., 192.168.x.1–x.10 excluded)
- **Inter-VLAN Routing**: Router-on-a-stick for Sales/Servers (subinterfaces Gig0/2.30, Gig0/2.99) and physical interfaces for HR/IT (Gig0/0, Gig0/1)
- **Switch Port Configuration**: Access ports for end devices and HR/IT uplinks; trunk port for Sales/Servers uplink
- **Port Security**: Configured on access ports to limit MAC addresses
- **Troubleshooting**: Verified with `ping`, `show ip dhcp binding`, `show vlan brief`, `show interfaces trunk`, `show interface status`.

## How to Use

1. Open `EnterpriseNetwork.pkt` in Cisco Packet Tracer (version 8.2 or later recommended).
2. Review configuration files in the `configs/` directory for router and switch settings.
3. Refer to `topology-diagram.png` for a visual representation of the network.
4. Follow troubleshooting notes in `docs/troubleshooting.md` for common issues.

## Testing Performed

- **DHCP Assignment**: Verified IP allocation using `show ip dhcp binding` on the router.
- **Intra-VLAN Connectivity**: Confirmed with `ping` within HR, IT, Sales, and Servers VLANs.
- **Inter-VLAN Communication**: Tested connectivity (e.g., HR PC to Sales PC, Sales PC to Server) via router interfaces.
- **Troubleshooting**: Addressed APIPA errors, VLAN misconfigurations, and port status issues using `show ip interface brief`, `show vlan brief`, and `show interfaces trunk`.

## Potential Enhancements

- **Internet Access**: Implement NAT on an additional router interface for external connectivity.
- **Redundancy**: Configure HSRP or VRRP for router failover.
- **Layer 3 Switching**: Migrate inter-VLAN routing to a Layer 3 switch using SVIs for improved performance.
- **Security**: Add a Cisco ASA firewall or ACLs to restrict inter-VLAN traffic.
- **Monitoring**: Enable SNMP or syslog for real-time network monitoring.

## License

This project is for educational and portfolio purposes only. Configurations and documentation are provided as-is for learning and demonstration.
