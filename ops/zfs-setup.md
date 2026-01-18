# ZFS setup
## Pools
### tank
- Purpose: critical data
- Layout: mirror
- Disks: 2 × 2 TB
- **Properties:**  
  - `ashift=12`  
  - `autotrim=on`

### media
- Purpose: non-critical Jellyfin media
- Layout: single disk
- Disks: 1 old HDD

## Dataset creation
Datasets are created by function, not by application.

### tank datasets
- photos
  - `recordsize=256K`
    - Reden: mix van grote originele foto’s en kleine thumbnails. 256K is groot genoeg voor foto’s, klein genoeg om thumbnails efficiënt te schrijven.
  - `logbias=throughput`  
- **documents**  
  - `recordsize=128K`
    - Reden: veel kleine files (txt, pdf, office), random access belangrijk. Te grote blokken zouden veel “waste” veroorzaken.

- **ebooks**  
  - `recordsize=128K`  
    - Reden: bestanden meestal klein, maar 128K is ruim voldoende om één bestand per blok te hebben. Efficiënt en past bij documents.
- **backups**  
  - `recordsize=1M`  
    - Reden: bestanden bestaan uit gemixte grootte (documents, configs, media). Kleinere blokken = efficiënter voor snapshots en ZFS send/receive.
  - `logbias=throughput`  
- **knowledge**  
  - `recordsize=64K`
    - Reden: veel tekstbestanden, wiki’s, notities. Kleinere blokken = sneller random access, minder write amplification bij kleine wijzigingen.  
- **configs**  
  - `recordsize=16K`
    - Reden: zeer kleine config-bestanden, soms slechts enkele KB. Klein recordsize voorkomt dat een kleine wijziging een groot blok herschrijft.

  
> Alle tank-datasets erven de pool-eigenschappen tenzij expliciet overschreven.


### media datasets
- media
  - `recordsize=1M` (optioneel, voor grotere media-bestanden)  

## ZFS properties
### Pool-wide (tank)
- `compression=lz4`  
- `atime=off`  
- `xattr=sa`  
- `acltype=posixacl`  

### Dataset-specific
- `recordsize` en `logbias` zoals hierboven vermeld  

## Snapshots
- Enabled for all datasets in `tank`
- Disabled for `media`

## Scrubbing
- Monthly scrub scheduled for all pools