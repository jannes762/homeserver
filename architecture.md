# Architecture

## Overview

- Hypervisor: Proxmox
- Filesystem: ZFS
- Virtualization: LXC by default, VM only when required
- Backup strategy: ZFS snapshots + Borg to Hetzner Storage Box

## Design principles

- Data is more important than services
- All persistent data lives on ZFS datasets
- Containers are disposable, datasets are not
- Critical and non-critical data are physically separated

## Virtualization choices

- LXC containers for most services
- VM only when:
  - OS-level control is required (e.g. Home Assistant OS)
  - Hardware passthrough requires it

## Services overview

### Core services
- Home Assistant (VM)
- Bitwarden / Vaultwarden
- Immich

### Archive & knowledge
- Paperless (documents)
- Calibre / Calibre Web (ebooks)
- Nextcloud (knowledge archive)
- Obsidian (knowledge editing)
- Karakeep
- Vikunja

### Media (non-critical)
- Jellyfin
- Radarr
- Sonarr
- Jackett
- qBittorrent

### Maybe / future
- TRIP


## Non-goals

- High availability
- Multi-node clustering
- Zero-downtime upgrades
- Enterprise-grade monitoring