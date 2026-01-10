# Homeserver

Platform: Proxmox VE  
Doel: self-hosted services + password manager

## Status
- In opbouw
- HDD's nog onderweg

## Services (gepland)
- Vaultwarden
- Reverse proxy
- Monitoring

# Homelab documentation

This repository documents the architecture, storage layout, services and
operational procedures of my home server.

Goals:
- Reliable storage using ZFS
- Clear separation between critical and non-critical data
- Automated backups to an offsite location
- Minimal exposure to the internet
- Reproducible setup through documentation

The server is built around Proxmox with mostly LXC containers and ZFS-backed
datasets mounted directly into containers.

# Homelab documentation

This repository contains the full documentation of my homelab setup.
It is organized by architecture, design decisions, operational procedures
and individual services.

---

## Architecture

- [Architecture overview](architecture.md)
- [Storage layout](storage.md)
- [Network design](network.md)

---

## Design decisions

- [Virtualization strategy](decisions/virtualization.md)
- [Naming conventions](decisions/naming.md)
- [Backup strategy](decisions/backups.md)
- [Network exposure](decisions/network-exposure.md)

---

## Operations

- [Proxmox installation](ops/proxmox-install.md)
- [ZFS setup](ops/zfs-setup.md)
- [LXC creation](ops/lxc-creation.md)
- [Upgrade strategy](ops/upgrade-strategy.md)
- [Backup and restore](ops/backup-restore.md)
- [Disaster recovery](ops/disaster-recovery.md)
- [Security hardening](ops/security-hardening.md)
- [Monitoring](ops/monitoring.md)
- [Disk health check](ops/disk-health-check.md)

---

## Services

### Core
- [Home Assistant](services/home-assistant.md)
- [Immich](services/immich.md)
- [Bitwarden](services/bitwarden.md)

### Archive & knowledge
- [Paperless](services/paperless.md)
- [Nextcloud](services/nextcloud.md)
- [Calibre](services/calibre.md)
- [Karakeep](services/karakeep.md)
- [Vikunja](services/vikunja.md)
- [Obsidian](services/obsidian.md)

### Media (non-critical)
- [Jellyfin](services/jellyfin.md)
