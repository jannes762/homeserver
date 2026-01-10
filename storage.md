# Storage

## Physical disks

### New disks
- 2 × 2 TB HDD
- Used for critical data
- Configured as a ZFS mirror

### Old disks
- 2 × 1 TB (non-identical)
- 1 × 320 GB
- Only one disk installed initially (SATA slot limitation)
- Used exclusively for non-critical media data

## ZFS pools

### tank
- Type: mirror
- Disks: 2 × 2 TB
- Purpose: critical and backed-up data

### media
- Type: single disk
- Disks: 1 old HDD
- Purpose: Jellyfin media
- No backups

## Dataset naming conventions

Datasets are named by function, not by application.

Examples:
- photos
- documents
- media
- ebooks
- backups