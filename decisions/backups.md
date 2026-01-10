# Backup strategy
## Principles
- Backups protect data, not applications
- Only critical datasets are backed up
- Media is explicitly excluded

## Tooling
- BorgBackup
- Remote target: Hetzner Storage Box

## What is backed up
From pool `tank`:
- photos
- documents
- ebooks
- knowledge
- configs

## What is not backed up
- media pool
- Jellyfin cache
- Temporary or regenerable data

## Backup frequency
- Daily for configs and documents
- Weekly for photos and ebooks

## Rationale
ZFS snapshots protect against local mistakes.
Borg provides offsite protection against hardware loss or disaster.