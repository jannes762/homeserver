# Tailscale operations

## Overview

Tailscale provides secure remote access to internal services using WireGuard tunnels.
It is used as an access VPN only.

## Installed nodes

| Node     | Type | Purpose |
|----------|------|---------|
| immich   | LXC  | Immich service access |
| proxmox  | Host | (Optional) administrative access |

## Autostart configuration

Tailscale must start automatically after reboot.

On each node running Tailscale:

```bash
systemctl enable tailscaled
systemctl start tailscaled
```

Persistent state is stored in:
`/var/lib/tailscale/`
No re-authentication is required after reboot.

## LXC requirements (Proxmox)
When running Tailscale inside a Proxmox LXC container:
`/dev/net/tun` must be available inside the container
Container can be privileged or unprivileged
Required configuration on the Proxmox host (`/etc/pve/lxc/<CTID>.conf`):
```bash
lxc.cgroup2.devices.allow: c 10:200 rwm
lxc.mount.entry: /dev/net/tun dev/net/tun none bind,create=file
```

After modifying the config:
```bash
pct restart <CTID>
```

 ## MagicDNS
MagicDNS is enabled in the Tailscale admin console.
Effect:
- Each node is reachable by hostname
- No IP addresses need to be documented or remembered
Example: `http://immich:2283`


## ACL model (high level)
Policy:
- Admin: unrestricted access
- Non-admin users: Immich-only

Implementation:
- Use MagicDNS hostnames
- Use device tags for least privilege

## Mobile usage notes
- Tailscale uses split tunneling by default
- Only traffic to Tailscale nodes goes through the tunnel
- It is not a replacement for privacy VPNs (e.g. NordVPN)

Android:
- Only one VPN can be active at a time
- Typically leave Tailscale enabled
- Use NordVPN only when needed

## Troubleshooting
### tailscaled fails to start in LXC
Likely cause:
- Missing `/dev/net/tun` inside LXC
- Check in the container:
```bash
ls -l /dev/net/tun
journalctl -u tailscaled --no-pager -n 120
```

### Cannot reach Immich
Check:
- Tailscale is connected on client and server
- Correct hostname (immich)
- Immich is listening on 0.0.0.0:2283
- ACL allows access