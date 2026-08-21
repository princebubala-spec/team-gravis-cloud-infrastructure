# VyOS DHCP Relay - Example Config (Generalized)

```
set service dhcp-relay listen-interface 'eth1'      # client-facing/gateway interface
set service dhcp-relay upstream-interface 'eth0'     # interface toward DHCP server
set service dhcp-relay server '10.0.20.4'            # remote site DHCP server IP
```

Notes:
- listen-interface = interface where relay listens for client broadcasts (the subnet's default gateway).
- upstream-interface = path toward the DHCP server (WAN/uplink side).
- Each site's router points to its local or remote DHCP server(s) depending on design (per-site vs cross-site failover).
