# Access control (Tailscale ACLs)

## Purpose

This document describes the intended access control model for the homelab.
Enforcement is done via Tailscale ACLs.

This file documents the **design**, even if ACLs are not yet applied.

## Security model

- Default deny
- Access is granted explicitly
- No service is reachable unless allowed
- Human-readable hostnames are used (MagicDNS)

## Roles

### Admin
- Full access to all Tailscale nodes
- SSH access
- Web interfaces (Proxmox, Immich, etc.)

### Immich-only users (e.g. family)
- Access limited to Immich web interface
- No SSH access
- No access to Proxmox or other services

## Naming conventions

- Immich service node: `immich`
- Proxmox host: `proxmox`
- Hostnames are resolved via Tailscale MagicDNS

## Planned ACL structure

### Admin access

Admins are allowed unrestricted access.

Conceptual rule:
- Source: admin users
- Destination: any node, any port

### Immich-only access

Non-admin users should only be able to access Immich.

Conceptual rule:
- Source: tagged devices (e.g. `immich-only`)
- Destination: `immich:2283`

## Tags

Tags are used to avoid relying on user roles alone.

Planned tag:
- `tag:immich-only`

Only admins are allowed to assign tags.

## Example ACL (not yet applied)

This is a **reference example**, not necessarily active.

```json
{
  "tagOwners": {
    "tag:immich-only": ["autogroup:admin"]
  },
  "acls": [
    {
      "action": "accept",
      "src": ["autogroup:admin"],
      "dst": ["*:*"]
    },
    {
      "action": "accept",
      "src": ["tag:immich-only"],
      "dst": ["immich:2283"]
    }
  ]
}

## Notes
 - ACLs are enforced centrally via the Tailscale admin console
 - No firewall rules are required on the hosts themselves
 - MagicDNS names should be preferred over IP addresses