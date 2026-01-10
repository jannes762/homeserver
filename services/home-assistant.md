# Home Assistant

## Purpose

Home Assistant is used for home automation and integrations with local devices.
It is considered a core service.

## Virtualization

- Virtual machine (VM)
- Home Assistant OS

## Rationale for VM usage

Home Assistant OS expects:
- Full control over the OS
- Supervisor-managed updates
- Add-on ecosystem

These requirements make a VM the most robust and least error-prone choice.

## Storage

- VM disk on SSD-backed storage
- Configuration stored inside the VM

## Data classification

- Configuration files
- Integration settings
- Automation logic

Data is considered critical but relatively small.

## Backups

- Home Assistant internal backups enabled
- VM-level snapshots optional
- External backup of HA backups recommended via dataset mount or export

## Restore strategy

1. Recreate VM
2. Restore Home Assistant backup
3. Verify integrations and automations

## Notes

Home Assistant is the only intentional exception to the LXC-first rule.
