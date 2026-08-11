# Network Plan

This document summarizes the anonymized network design used across the two simulated client sites in the Team Gravis lab.

## Site Overview

| Site | Client | Role |
|---|---|---|
| Site 1 | Client A | Windows-based environment (AD, DNS, DHCP, DFS) |
| Site 2 | Client B | Open-source / Linux-based environment (web, DMZ services) |

## VLAN / Subnet Plan (example segmentation)

| VLAN | Purpose | Subnet | Gateway |
|---|---|---|---|
| 10 | Users | 10.10.10.0/24 | 10.10.10.1 |
| 20 | Servers | 10.10.20.0/24 | 10.10.20.1 |
| 30 | Management | 10.10.30.0/24 | 10.10.30.1 |
| 40 | DMZ | 10.10.40.0/24 | 10.10.40.1 |

Each site follows the same segmentation pattern, with distinct subnet ranges per site to avoid overlap across the WireGuard site-to-site tunnel.

## Routing
- VyOS virtual routers provide inter-VLAN routing at each site.
- DHCP relay is configured on VyOS to forward client DHCP requests to the centralized DHCP server across routed subnets.
- Site-to-site connectivity is secured using WireGuard tunnels between site routers.

## DNS
- Internal DNS is provided by the Windows Server domain controller for the Windows-based client environment.
- DNS forwarders handle external name resolution.

## DMZ
- A dedicated DMZ VLAN hosts externally facing services (e.g., web server) separate from internal user and server VLANs.
- Firewall rules restrict DMZ traffic from reaching internal management and server segments directly.

## Notes
All addressing shown here is representative and has been generalized/anonymized from the original project documentation for public publication.
