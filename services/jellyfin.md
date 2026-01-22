# Jellyfin

## Purpose
Self-hosted media streaming service for movies and series.
Acts as the **playback layer** of the media stack.

Media content is considered **ephemeral** and **non-critical**.
Reinstallation is preferred over recovery.

---

## Virtualization
- Proxmox LXC container
- Docker running inside the LXC
- Jellyfin runs as a Docker container

---

## Storage
- ZFS pool: `media`
- Dataset: `media/media`
- Mounted into the LXC at `/data/media`
- Subdirectories:
  - `/data/media/movies`
  - `/data/media/series`
  - `/data/media/downloads`

Storage is shared with the *arr stack (Sonarr, Radarr, qBittorrent, Bazarr).

---

## Networking
- Exposed via HTTP
- Port: `8096`
- Accessible via Tailscale MagicDNS

---

## Backups
- None

Rationale:
- Media files are reproducible
- Downloads can be recreated automatically
- Backup cost > recovery cost

---

## Related Services (Media Stack)
- Sonarr – series management
- Radarr – movie management
- Prowlarr – indexer management
- qBittorrent – download client
- Bazarr – subtitle management
- Overseerr – optional request / discovery frontend

All services are deployed via Docker in the same LXC.

---

## Notes
- Jellyfin does **not** manage downloads or files
- File organization and lifecycle are handled by Sonarr/Radarr
- User-facing UI only; no critical state stored here
