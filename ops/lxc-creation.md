# LXC creation

## Goal

Provide a consistent and reproducible way to create LXC containers in Proxmox.

## General principles

- LXC by default
- Containers are disposable
- Persistent data always lives on ZFS datasets
- Containers never own important data

## Base template

- Debian stable (recommended)
- Minimal installation
- No desktop environment

## Container settings

- Privileged: no (unless strictly required)
- Unprivileged: yes
- Nesting: enabled when Docker is used inside LXC
- Features:
  - keyctl: enabled if needed
  - fuse: enabled when required

## Storage layout

- Root filesystem on SSD-backed storage
- Persistent data mounted from ZFS datasets

Example mounts:
- /data/photos → tank/photos
- /data/documents → tank/documents
- /data/media → media/media

## Networking

- Single network interface
- Bridge: vmbr0
- DHCP or static IP depending on service criticality

## Backups

- Proxmox container backups enabled only for:
  - configuration
  - container metadata
- Data is backed up via ZFS + Borg, not via Proxmox backups

## Rationale

Separating containers from data allows:
- Fast redeployment
- Simple recovery
- Minimal coupling between services and storage
