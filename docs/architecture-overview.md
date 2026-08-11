# Architecture Overview

## Purpose
This document describes the overall infrastructure architecture built for the Team Gravis lab: a simulated MSP supporting two anonymized client environments (Client A and Client B) across two network sites.

## High-Level Design
- Two sites, each with segmented VLANs for users, servers, management, and DMZ.
- Site-to-site connectivity secured via a WireGuard tunnel.
- Virtualization platform: Proxmox VE, hosting all routers, servers, and client VMs.
- Routing and DHCP relay handled by VyOS virtual router appliances.

## Client A Environment (Windows-based)
- Active Directory Domain Services for centralized identity management.
- DNS for internal name resolution, with forwarders for external resolution.
- DHCP for dynamic addressing, including DHCP relay across routed VLANs.
- DFS for centralized/replicated file storage.

## Client B Environment (Open-source / Linux-based)
- Linux-based servers providing web and application services.
- DMZ-hosted services accessible from outside the internal network, isolated from core internal VLANs.

## Storage
- TrueNAS used for centralized storage supporting backup and shared file services.

## Connectivity
- WireGuard site-to-site tunnel links the two sites securely over the WAN.
- VyOS routers act as the tunnel endpoints and handle inter-VLAN routing at each site.

## DHCP Relay Flow
1. Client device on a routed VLAN broadcasts a DHCP request.
2. VyOS router (configured as a DHCP relay agent) forwards the request to the central DHCP server.
3. DHCP server responds with an offer, which VyOS relays back to the client.
4. Client receives an IP address, gateway, and DNS configuration scoped to its VLAN.

## DMZ Design
- Externally facing services are placed on a dedicated DMZ VLAN.
- Firewall rules limit traffic between the DMZ and internal management/server VLANs.

## Diagram
A topology diagram will be added to `diagrams/topology.png` once team approval for publication is confirmed.

## Attribution
This architecture was designed and implemented collaboratively by Team Gravis. See `contribution-and-attribution.md` for individual contribution details.
