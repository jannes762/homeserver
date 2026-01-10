# Nextcloud

## Purpose

Nextcloud is used as a personal knowledge archive.
It stores historical school documents, slides, papers and related files.

Nextcloud is not considered a real-time collaboration platform but a structured
file archive with web access.

## Virtualization

- LXC container

## Storage

- ZFS pool: tank
- Dataset: knowledge

Mounted path:
- /data/knowledge → tank/knowledge

## Data classification

- PDFs
- Slides
- Text documents
- Reference material

All data is considered critical.

## Backups

- knowledge dataset included in Borg backups
- Daily ZFS snapshots enabled

## Restore strategy

1. Recreate LXC container
2. Mount knowledge dataset
3. Restore dataset from Borg if needed

Nextcloud-specific configuration is secondary to data recovery.

## Notes

If Nextcloud is ever replaced, the knowledge dataset remains usable without
migration.
