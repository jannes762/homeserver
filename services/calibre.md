# Calibre / Calibre Web

## Purpose

Management and access to an ebook library.
Calibre Web is used as the primary user interface.

## Virtualization

- LXC container

## Storage

- ZFS pool: tank
- Dataset: ebooks

Mounted path:
- /data/ebooks → tank/ebooks

## Data classification

- Ebook files
- Metadata

All data is considered critical.

## Backups

- ebooks dataset included in Borg backups
- Weekly offsite backups
- Daily ZFS snapshots

## Restore strategy

1. Recreate LXC container
2. Mount ebooks dataset
3. Restart service

## Notes

Calibre is treated as a frontend to the ebooks dataset.
The dataset remains usable without Calibre.
