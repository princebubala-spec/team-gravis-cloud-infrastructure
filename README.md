# Team Gravis — Multi-Site Cloud Infrastructure Lab

## Overview
A collaborative academic project simulating a Managed Service Provider (MSP) supporting two client environments across separate network sites. The lab covers virtualization, network segmentation, routing, directory services, storage, and secure site-to-site connectivity.

Client names have been anonymized for public publication.

## Environment Summary

| Client | Platform Focus | Core Services |
|---|---|---|
| Client A | Windows-based | Active Directory, DNS, DHCP, DFS |
| Client B | Open-source / Linux-based | Linux services, web/DMZ hosting |

## Technologies Used
- Proxmox VE (virtualization)
- VyOS (routing, DHCP relay)
- Windows Server (AD DS, DNS, DHCP, DFS)
- Linux server services
- TrueNAS (storage)
- WireGuard (site-to-site connectivity)
- VLAN segmentation / multi-site network design

## Architecture Highlights
- Two-site network design with segmented VLANs per site
- Inter-site connectivity secured via WireGuard
- Centralized and relayed DHCP across routed subnets
- Domain services and DNS supporting the Windows-based client environment
- Dedicated DMZ segment for externally facing services

## My Contributions
- Deployed VyOS router virtual machines in the Proxmox environment
- Configured and validated DHCP relay across routed network segments
- Worked on Windows Server infrastructure services, including DHCP, DNS, and DFS
- Participated in multi-site service testing, troubleshooting, and documentation

## Team Scope
This was a collaborative academic project completed by Team Gravis. Routing architecture, firewall policy, VPN connectivity, directory services, storage, backup, Linux services, DMZ services, and final documentation were implemented collaboratively across the team.

## Repository Structure
```
team-gravis-cloud-infrastructure/
├── README.md
├── docs/
│   ├── architecture-overview.md
│   ├── network-plan.md
│   └── contribution-and-attribution.md
├── diagrams/
│   └── topology.png 
├── screenshots/
│   └── (pending permission)
└── configs/
    └── (sanitized snippets only)
```

## Status
Diagrams and screenshots will be added once team approval is confirmed.
