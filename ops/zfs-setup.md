# ZFS setup
## Pools
### tank
- Purpose: critical data
- Layout: mirror
- Disks: 2 × 2 TB

### media
- Purpose: non-critical Jellyfin media
- Layout: single disk
- Disks: 1 old HDD

## Dataset creation
Datasets are created by function, not by application.

### tank datasets
- photos
- documents
- ebooks
- backups
- knowledge
- configs

### media datasets
- media

## ZFS properties
- compression: on
- atime: off
- recordsize:
  - documents / ebooks: default
  - media: large recordsize

## Snapshots
- Enabled for all datasets in `tank`
- Disabled for `media`

## Scrubbing
- Monthly scrub scheduled for all pools