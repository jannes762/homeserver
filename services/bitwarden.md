# Bitwarden (Vaultwarden)

## Purpose

Password manager for personal credentials.
This service contains highly sensitive data.

## Virtualization

- LXC container

## Storage

- ZFS pool: tank
- Dataset: configs

Mounted paths:
- /data/configs/bitwarden → tank/configs/bitwarden

## Data classification

- Encrypted password vault
- Configuration files
- Encryption keys

All data is critical and sensitive.

## Backups

- configs dataset included in Borg backups
- Daily backups
- Encrypted both at rest and in transit

## Restore strategy

1. Recreate LXC container
2. Mount configs dataset
3. Restore dataset from Borg
4. Restart service

## Security notes

- Service should not be exposed directly to the internet
- Access via VPN preferred
- Strong master password required

Bitwarden is considered a single point of failure if mismanaged.
