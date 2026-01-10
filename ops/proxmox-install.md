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
