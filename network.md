# Network

## Current setup

- ISP: Telenet
- Router: ISP-provided router
- Public IPv4: none (CGNAT)
- IPv6: not relied upon
- Port forwarding: not used / not possible

## Exposure strategy

- No direct exposure of services by default
- No port forwarding
- No UPnP
- All remote access is performed via encrypted tunnels


## Remote access

- Implemented using **Tailscale**
- Works outbound (CGNAT-safe)
- No public IP required
- No open ports on the router

Related docs:
- `/decisions/remote-access.md`
- `/ops/tailscale.md`

## Domain

- No public domain required
- Internal naming provided by Tailscale MagicDNS