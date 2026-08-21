# Windows DHCP Scope Notes (Generalized)

This reflects a full cross-site failover design: both DHCP servers hold
scopes for both sites, and VyOS relays forward client requests to both
servers. IPs below are generalized placeholders (not the real lab addressing).

DHCP Server A (10.0.10.4):

- Scope A: 10.0.10.0/27
  - Router option 003: 10.0.10.1
  - Exclusions: .1-.3 (infra reservations)
  - Range: .10-.30
- Scope B: 10.0.20.0/26
  - Router option 003: 10.0.20.1
  - Range: .6-.62

DHCP Server B (10.0.20.4):

- Same two scopes (10.0.10.0/27 and 10.0.20.0/26), configured in DHCP
  failover with Server A.

Design notes:

- Each VyOS router relays client broadcasts to both DHCP servers.
- The server matches the GIADDR (relay/gateway IP) to the correct scope,
  regardless of which server physically responds.
- Failover (load-balance or hot-standby) determines which server answers
  each request and keeps lease state in sync between the two servers.
- Simpler alternative: one scope per site, hosted only on that site's local
  server (no cross-site failover), if higher availability isn't required.
