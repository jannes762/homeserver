# Disk health check

## When

- Before adding any disk to a ZFS pool
- For both new and old disks

## Steps

1. SMART short test
2. SMART long test
3. Review SMART attributes
4. Optional: read-only badblocks test (time permitting)

Disks that fail any step are not used for critical data.

# HDD Testen voor gebruik

## Doel
Zeker zijn dat de harde schijven geen fouten bevatten voordat ze in ZFS mirror gaan.

## Stappen
1. Sluit de HDD aan op server (server uit voordat je ze plaatst).
2. Controleer dat de schijf herkend wordt:
   ```bash
   lsblk
   ```
3. SMART info bekijken:
   ```bash
   smartctl -a /dev/sdX
   ```
   Controleer: Reallocated_Sector_Ct = 0, Pending_Sectors = 0, geen errors.

4. SMART long test:
   ```bash
   smartctl -t long /dev/sdX
   ```
   - duurt 4–8 uur
   - status controleren:
   ```bash
   smartctl -a /dev/sdX
   ```
5. (Optioneel) Badblocks light test:
   ```bash
   badblocks -sv /dev/sdX
   ```
   - detecteert vroege fouten, duurt uren

## Tips
- Niet installeren op schijven met fouten.
- Pas na deze tests de ZFS mirror aanmaken.