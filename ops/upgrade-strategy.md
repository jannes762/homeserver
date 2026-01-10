# Upgrade strategy

## Scope

This document describes how system and service upgrades are handled.

## Proxmox upgrades

- Minor updates applied regularly
- Major upgrades planned and documented
- ZFS pools verified before and after upgrades

## Container upgrades

- Containers are upgraded individually
- Rollback via snapshots if needed
- Containers may be recreated instead of upgraded

## Service upgrades

- Prefer in-place upgrades when supported
- Configuration stored outside containers
- Data always protected by snapshots

## ZFS considerations

- No pool upgrades without full backup
- Scrub before major changes

## Rationale

Upgrades should never put data at risk.
Recreation is preferred over complex rollback procedures.
