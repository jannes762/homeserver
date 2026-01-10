# Immich
## Purpose
Photo and video management with mobile sync.

## Virtualization
- LXC container

## Storage
- photos dataset:
  - Originals
  - Uploads
- Database stored on SSD-backed storage

## Backups
- photos dataset included in Borg backups
- Database and configuration included

## Notes
Photos are considered high-value personal data.
Immich is treated as a replaceable frontend for the photos dataset.