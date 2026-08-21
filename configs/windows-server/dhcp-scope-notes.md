# Windows DHCP Scope Notes (Generalized)

Site A scope: 10.0.10.0/27
  - Gateway: 10.0.10.1
  - Exclusions: .1-.3 (infra reservations)
  - Range: .10-.30

Site B scope: 10.0.20.0/26
  - Gateway: 10.0.20.1
  - Range: .6-.62

Design: one scope per site/subnet, hosted on that site's local DHCP server.
Optional enhancement: per-subnet failover if both servers can reach both VLANs via relay.
