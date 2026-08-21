# VyOS DHCP Relay - Example Config (Generalized)

This example shows a full cross-site failover relay design, where both DHCP
servers can lease addresses for both sites. IPs below are generalized
placeholders (not the real lab addressing).

## Windows DHCP scopes (conceptual)

- DHCP Server A (10.0.10.4):
  - Scope A: 10.0.10.0/27 (router option 003 = 10.0.10.1)
  - Scope B: 10.0.20.0/26 (router option 003 = 10.0.20.1)
- DHCP Server B (10.0.20.4): same two scopes, in failover with Server A

## Site 1 VyOS router (clients on 10.0.10.0/27)

```
configure
set interfaces ethernet eth1 address '10.0.10.1/27'   # Site 1 gateway
set interfaces ethernet eth0 address '10.10.1.1/24'    # WAN/server LAN toward both DHCP servers

set service dhcp-relay listen-interface 'eth1'
set service dhcp-relay upstream-interface 'eth0'
set service dhcp-relay server '10.0.10.4'
set service dhcp-relay server '10.0.20.4'

commit
save
exit
```

## Site 2 VyOS router (clients on 10.0.20.0/26)

```
configure
set interfaces ethernet eth1 address '10.0.20.1/26'    # Site 2 gateway
set interfaces ethernet eth0 address '10.10.2.1/24'    # WAN/server LAN toward both DHCP servers

set service dhcp-relay listen-interface 'eth1'
set service dhcp-relay upstream-interface 'eth0'
set service dhcp-relay server '10.0.10.4'
set service dhcp-relay server '10.0.20.4'

commit
save
exit
```

## Notes

- listen-interface = interface where relay listens for client broadcasts (the subnet's default gateway).
- upstream-interface = path toward the DHCP server(s) (WAN/uplink side).
- In this cross-site failover design, a Site 1 client's DISCOVER is relayed with GIADDR = 10.0.10.1 to both servers; each server matches the GIADDR to the 10.0.10.0/27 scope, and failover decides which server replies. Site 2 works the same way with GIADDR = 10.0.20.1 and the 10.0.20.0/26 scope.
- Simpler alternative: point each router only at its local DHCP server for per-site-only DHCP (no cross-site failover).
