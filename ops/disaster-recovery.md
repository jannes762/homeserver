# Disaster recovery

## Scope

This document describes recovery procedures for catastrophic failures.

## Scenarios covered

- Single disk failure
- ZFS pool failure
- Complete server loss
- Offsite restore from Hetzner

## Single disk failure (tank)

1. Replace failed disk
2. Attach new disk to pool
3. Allow ZFS to resilver
4. Monitor resilvering process

No data loss expected.

## Pool failure

1. Stop all containers
2. Recreate ZFS pool
3. Restore datasets from Borg
4. Reattach datasets to containers

## Complete server loss

1. Install Proxmox on new hardware
2. Recreate ZFS pools
3. Install Borg
4. Restore datasets from Hetzner
5. Recreate LXC containers
6. Mount restored datasets

## Design assumption

Recovery prioritizes data.
Services are reinstalled, not restored.

## Recovery time objective

- Data availability prioritized over service uptime
- Acceptable downtime: hours to days
