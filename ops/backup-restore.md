# Backup and restore

## Scope

This document describes backup and restore procedures for critical data.

## Backup layers

### Layer 1: ZFS snapshots

- Protect against accidental deletion
- Fast local rollback
- Enabled on all datasets in pool `tank`

### Layer 2: Offsite backups

- Tool: BorgBackup
- Target: Hetzner Storage Box
- Encrypted repositories

## Included datasets

- photos
- documents
- ebooks
- knowledge
- configs

## Excluded datasets

- media
- caches
- temporary data

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

### Full server loss

1. Reinstall Proxmox
2. Recreate ZFS pools
3. Restore datasets from Borg
4. Recreate LXC containers
5. Reattach datasets

## Rationale

The system is designed so that restoring data automatically restores services.
Application state is never the primary recovery target.
