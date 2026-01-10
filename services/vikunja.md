# Vikunja

## Purpose

Task and project management.
Used for personal planning and lightweight project tracking.

## Virtualization

- LXC container

## Storage

- ZFS pool: tank
- Dataset: knowledge

Mounted paths:
- /data/knowledge/vikunja → tank/knowledge/vikunja

## Data classification

- Tasks
- Projects
- Metadata

Data is useful but not mission-critical.

## Backups

- knowledge dataset included in Borg backups
- Daily ZFS snapshots enabled

## Restore strategy

1. Recreate LXC container
2. Mount knowledge dataset
3. Restore dataset from Borg if needed

## Notes

Vikunja can be replaced without impacting other services.
