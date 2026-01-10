# Proxmox installation

## Goal

Install Proxmox as the base hypervisor with ZFS support and prepare the system
for container-based workloads.

## Installation notes

- Install Proxmox on the SSD
- Use default ZFS-on-root layout
- No additional disks connected during initial installation

## Post-install steps

- Update system
- Configure host name
- Enable subscription-free repositories
- Disable enterprise repository

## Networking

- Single bridge (vmbr0)
- DHCP initially
- Static IP configured after installation

## Rationale
Proxmox is used as a stable base layer. All application state is externalized
to ZFS datasets, making containers disposable.


# Installatie Fases

## Fase 1 — Proxmox op SSD
- BIOS check: virtualization aan, secure boot uit
- Boot vanaf USB installer
- Installeer Proxmox op SSD
- Vast IP instellen
- Updates & SSH testen

## Fase 2 — Basisconfiguratie
- non-subscription repo activeren
- test container (optioneel)

## Fase 3 — HDD Plaatsen & Testen
- Server uit
- Plaats HDDs
- Volg HDD_TESTS.md

## Fase 4 — ZFS Mirror & Datasets
- Maak ZFS mirror aan in Proxmox GUI
- Maak datasets:
    - tank/photos
    - tank/appdata
    - tank/media
    - tank/backups
- Compression on, atime off

## Fase 5 — Containers & VM’s
- Immich → tank/photos
- Bitwarden → tank/appdata
- Media → tank/media

## Fase 6 — Snapshots & Monitoring
- Dagelijkse snapshots appdata
- Wekelijkse snapshots photos
- Maandelijks: zpool scrub tank