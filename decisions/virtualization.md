# Virtualization strategy

## Goal

Define the virtualization approach for the homelab and rationale for choices.

## Principles

- LXC containers are preferred for most services
- VM only used when strictly required

## LXC

### Pros

- Lightweight and efficient
- Direct ZFS dataset mounts
- Easy snapshots and restoration
- Fast to redeploy

### Cons

- Limited OS-level isolation
- Some software may require full OS

## VM

### Pros

- Full OS control
- Needed for services with OS-level dependencies (e.g., Home Assistant OS)
- Better isolation for critical or complex applications

### Cons

- More disk and memory overhead
- Slower deployment
- Less direct ZFS integration

## Decision table

| Service                  | LXC / VM | Reason |
|---------------------------|----------|--------|
| Home Assistant            | VM       | OS-level control & Supervisor required |
| Bitwarden / Vaultwarden   | LXC      | Lightweight, can use dataset mount |
| Immich                    | LXC      | Lightweight, data separation |
| Paperless                 | LXC      | Lightweight, data on tank dataset |
| Calibre / Calibre Web     | LXC      | Lightweight, uses ZFS datasets |
| Nextcloud                 | LXC      | Lightweight, dataset-backed |
| Karakeep                  | LXC      | Lightweight, dataset-backed |
| Vikunja                   | LXC      | Lightweight, dataset-backed |
| Jellyfin / Radarr / Sonarr / Jackett / qBittorrent | LXC | Non-critical, lightweight |

## Rationale

- Default to LXC for efficiency and simplicity
- Use VM only when unavoidable for stability or OS dependency
- All data remains on ZFS, so containers or VMs are disposable
