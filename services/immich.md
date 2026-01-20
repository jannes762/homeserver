# Immich
## Purpose
Photo and video management with mobile sync.

## Virtualization
- LXC container

## Storage
- photos dataset:
  - Originals
  - Uploads
- Database stored on SSD-backed storage

## Backups
- photos dataset included in Borg backups
- Database and configuration included

## Notes
Photos are considered high-value personal data.
Immich is treated as a replaceable frontend for the photos dataset.

## Network access

Immich is not exposed to the public internet.

Access is provided via Tailscale:
- Encrypted WireGuard tunnel
- No open ports on the router
- Works behind CGNAT

The service is reachable at:

- URL: `http://immich:2283`
- Resolution: Tailscale MagicDNS

Direct access via public IP or port forwarding is intentionally not supported.

## Dependencies

- Docker (running inside LXC container `immich`)
- Tailscale (installed on the LXC host, not inside Docker)
- MagicDNS enabled in Tailscale

## Security notes

- Immich listens on `0.0.0.0:2283` inside the container
- Exposure is limited by Tailscale ACLs (planned / enforced centrally)
- No reverse proxy is used at this stage