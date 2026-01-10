# Jellyfin
## Purpose
Media streaming service for movies and series.
Content is ephemeral and not considered critical.

## Virtualization
- LXC container

## Storage
- ZFS pool: media
- Dataset: media/media
- Mounted directly into the container

## Backups
- None

## Notes
- Radarr, Sonarr, Jackett and qBittorrent are considered part of the same
  non-critical media stack.
- Reinstallation is preferred over recovery.
