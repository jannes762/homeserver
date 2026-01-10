# Security hardening

## Scope

This document describes baseline security measures for the homelab.
The focus is on reducing attack surface rather than achieving enterprise-level
hardening.

## Core principles

- Expose as little as possible
- Trust the local network, but verify access
- Prefer simple and auditable configurations
- Security must not compromise recoverability

## Proxmox host

- Keep Proxmox updated
- Disable unnecessary services
- Use strong passwords or SSH keys
- Restrict root access to trusted machines

## Network exposure

- No services exposed by default
- VPN (WireGuard) preferred for remote access
- Port forwarding only when explicitly required
- Any exposed service must be documented

## Containers

- Unprivileged LXC containers by default
- Minimal base images
- No SSH access unless required
- Secrets stored outside containers when possible

## Storage security

- ZFS snapshots enabled for critical datasets
- Borg repositories encrypted
- Hetzner Storage Box accessed via SSH keys

## Credential management

- Bitwarden used as system of record for credentials
- Strong master password required
- Backups of Bitwarden data verified regularly

## Logging

- Default Proxmox and container logs retained
- No centralized logging initially
- Logging can be expanded if required

## Trade-offs

This setup favors:
- Low complexity
- Clear recovery paths
- Manual control

Over-automation and excessive security layers are intentionally avoided.
