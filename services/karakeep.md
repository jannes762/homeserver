# Karakeep

## Purpose

Personal inventory and tracking system.
Used for keeping track of owned items and related information.

## Virtualization

- LXC container

## Storage

- ZFS pool: tank
- Dataset: knowledge

Mounted paths:
- /data/knowledge/karakeep → tank/knowledge/karakeep

## Data classification

- Item records
- Notes
- Metadata

Data is considered important.

## Backups

- knowledge dataset included in Borg backups
- Daily ZFS snapshots enabled

## Restore strategy

1. Recreate LXC container
2. Mount knowledge dataset
3. Restore dataset from Borg if needed

## Notes

Karakeep is not a system of record for irreplaceable data,
but restoring it is preferred over re-entry.
