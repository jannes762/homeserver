# Backup strategy
## Principles
- Backups protect data, not applications
- Only critical datasets are backed up
- Media is explicitly excluded

## Tooling
- BorgBackup
- Remote target: Hetzner Storage Box

## What is backed up
From pool `tank`:
- photos
- documents
- ebooks
- knowledge
- configs

## What is not backed up
- media pool
- Jellyfin cache
- Temporary or regenerable data

## Backup frequency
- Daily for configs and documents
- Weekly for photos and ebooks

## Rationale
ZFS snapshots protect against local mistakes.
Borg provides offsite protection against hardware loss or disaster.

# Offsite Backup Strategie

## Doel
Zorg voor 3-2-1 backup, offsite voor kritische data, initieel en incremental.

## Tools
- BorgBackup
- Hetzner Storage Box

## Initiele Backup
- Splits data in datasets of directories:
    - /tank/photos (selectie)
    - /tank/appdata
- Borg init:
  ```bash
  borg init user@vps:/repo
  ```
- Maak init backup:
  ```bash
  borg create user@vps:/repo::init /tank/appdata /tank/photos
  ```
- Chunking automatisch, upload kan worden gepauzeerd/herstart

## Incremental Backup
- Dagelijks alleen gewijzigde bestanden:
  ```bash
  borg create user@vps:/repo::$(date +%Y-%m-%d) /tank/appdata /tank/photos
  ```

## Retentie & Pruning
- Retentiebeleid:
  - Dagelijks 7 dagen
  - Wekelijks 4 weken
  - Maandelijks 6 maanden
- Prune:
  ```bash
  borg prune -v --list --keep-daily=7 --keep-weekly=4 --keep-monthly=6 user@vps:/repo
  ```

## Tips
- Init backup kan offline via USB-stick of vanaf werk.
- Rest van de backups incrementals over thuisnetwerk.