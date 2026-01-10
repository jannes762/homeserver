# Obsidian

## Purpose

Obsidian is used as a personal note-taking and knowledge management tool.
It complements Nextcloud and the knowledge archive by allowing linked notes,
markdown editing, and personal organization.

## Virtualization

- LXC container (optional)
- Alternatively, can run on a local workstation accessing the ZFS knowledge dataset

## Storage

- ZFS pool: tank
- Dataset: knowledge

Mounted paths:
- /data/knowledge/obsidian → tank/knowledge/obsidian

## Data classification

- Markdown notes
- Linked knowledge
- Templates and personal references

All data is considered important, but easily reproducible from exported notes if lost.

## Backups

- knowledge dataset included in Borg backups
- Daily ZFS snapshots enabled

## Restore strategy

1. Recreate LXC container if used
2. Mount knowledge dataset
3. Restore dataset from Borg if needed
4. Restart Obsidian client or reconnect workspace

## Notes

- Obsidian itself is just a frontend; all critical data lives on the ZFS knowledge dataset.
- Multiple devices can access the same dataset via network mount if desired.
- Obsidian sync or third-party sync tools are optional; backup relies on ZFS + Borg.
