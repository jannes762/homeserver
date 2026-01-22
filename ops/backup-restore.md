# Backup and restore

## Scope

This document describes backup and restore procedures for critical data.
This includes:
- user-generated content (photos, documents, knowledge)
- service state required for recovery (databases)
- configuration required to reattach data to services

Application containers themselves are treated as disposable.


## Backup layers

### Layer 1: ZFS snapshots

- Protect against accidental deletion
- Fast local rollback
- Enabled on all datasets in pool `tank`

ZFS snapshots are not used for database consistency guarantees.
Databases are backed up using logical dumps instead.

### Layer 2: Offsite backups

- Tool: BorgBackup
- Target: Hetzner Storage Box
- Transport: SSH
- Encryption: Borg native encryption
- Repositories are accessed from the Proxmox host only

Offsite backups are split by data type:
- snapshot-based backups for large immutable data (photos)
- logical dumps for databases

## Included datasets

### Snapshot-backed datasets (ZFS → Borg)

- tank/photos
- tank/documents
- tank/ebooks
- tank/knowledge

These datasets are protected by:
- periodic ZFS snapshots (sanoid)
- Borg backups of snapshot contents

### Dump-backed data (logical backups)

- PostgreSQL database used by Immich

Database data is not backed up as raw files.
Instead, a daily pg_dump is created and backed up using Borg.


## Excluded datasets

- media
- caches
- temporary data

These datasets can be regenerated and do not contain unique state.
They are explicitly excluded to reduce backup size and complexity.

## Database backups

### Immich PostgreSQL database

- Database engine: PostgreSQL
- Deployment: Docker inside an LXC container
- Backup method: logical dump using pg_dump
- Execution context: Proxmox host (via pct exec)

### Dump location

- Host path: /rpool/data/immich-db-dumps
- This directory contains only dump files
- One dump file is kept locally; history is stored in Borg

### Backup characteristics

- Dump format: plain SQL
- Borg compression: zstd
- Borg deduplication enabled
- Retention managed independently from photo backups

Raw PostgreSQL data directories are never backed up.


## Restore scenarios

### Single file restore

1. Locate the snapshot or Borg archive
2. Restore file into dataset
3. Verify integrity

### Dataset restore

1. Stop affected containers
2. Restore dataset from Borg
3. Remount dataset
4. Restart containers

### Database restore (Immich)

1. Restore the desired Borg archive containing the database dump
2. Extract the SQL dump file
3. Stop the Immich application containers
4. Drop and recreate the database if needed
5. Restore using:
   psql immich < immich.sql
6. Restart containers


### Full server loss

1. Reinstall Proxmox
2. Recreate ZFS pools
3. Restore datasets from Borg
4. Recreate LXC containers
5. Reattach datasets

Application containers are not the primary recovery target.
Application state is restored through data and database recovery.


## Rationale

The system is designed so that restoring data automatically restores services.
Application state is never the primary recovery target.

## Automation

All backups are orchestrated from the Proxmox host.

- Individual backup scripts exist per data type
- A master script triggers all backups in sequence
- Execution is handled via cron

This design ensures:
- predictable execution order
- separation of concerns
- easy extension with additional services

## Implementation notes

Backup execution is handled by the following scripts on the Proxmox host:

- /root/borg-photos.sh
- /root/borg-immich-db.sh
- /root/borg-all.sh

Logs are written to:
- /var/log/borg-photos.log
- /var/log/borg-immich-db.log
- /var/log/borg-cron.log

All scripts must be executable (chmod +x).



### Failure handling

Backup scripts are designed to fail fast and log errors.
Partial failures (e.g. database backup failing while photo backup succeeds)
do not prevent other backup layers from completing.

## Troubleshooting

If a scheduled backup did not run:

1. Verify cron is running:
   systemctl status cron

2. Verify the cron entry exists:
   crontab -l

3. Check the cron log:
   tail /var/log/borg-cron.log

4. Verify scripts are executable:
   ls -l /root/borg-*.sh

5. Test in a cron-like environment:
   env -i bash -c '/root/borg-all.sh'
