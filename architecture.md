# Architectuur

## Virtualisatie
- Platform: Proxmox VE
- VM's voor internet-facing services
- LXC voor interne tools

## Services

- Vaultwarden
  - Type: VM
  - Runtime: Docker
  - Reden: secrets + publiek bereikbaar

- Monitoring
  - Type: LXC
  - Reden: intern, low-risk