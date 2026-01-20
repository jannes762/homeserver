# Remote access strategy

## Context

The homeserver runs behind an ISP-provided router with CGNAT.
Inbound connections from the public internet are not possible or reliable.

Primary goals:
- Secure remote access to the homelab
- No exposed ports by default
- No dependency on a public IPv4
- Minimal ongoing maintenance
- No mandatory monthly cost

## Decision

Remote access is implemented using **Tailscale**.

Tailscale provides:
- WireGuard-based encrypted tunnels
- NAT traversal (works behind CGNAT)
- No inbound port forwarding
- Identity-based access control (ACLs)
- Minimal operational overhead

Tailscale is used strictly for **access**, not as a privacy VPN.

## Scope

Tailscale is installed on:
- LXC container `immich` (primary service access)
- On the Proxmox host for administrative access

No Tailscale components run inside Docker containers.

## Alternatives considered

### WireGuard with VPS
- Rejected due to:
  - additional infrastructure
  - ongoing VPS cost
  - higher operational complexity

### Direct exposure with port forwarding
- Rejected due to:
  - CGNAT limitations
  - increased attack surface
  - higher maintenance burden

### Cloudflare Tunnel
- Considered as a **future option**
- Only for selectively exposing Immich to non-technical users
- Not part of the current baseline setup

## Security principles

- Default deny
- No public services exposed by default
- Access limited by device identity and ACLs
- Human-readable hostnames via MagicDNS
