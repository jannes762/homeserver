# Updaten

## Proxmox host
```
apt update
apt list --upgradable
apt full-upgrade
pveversion -v
```
Als er een nieuwe kernel is:
```
proxmox-boot-tool status
reboot
```

## LXC
```
apt update
apt full-upgrade
apt autoremove
apt autoclean
```

## Tailscale
```
tailscale up --force-reauth
```


## Docker
```
docker compose config
docker compose pull
docker compose up -d
docker ps
docker image prune
```

## Docker compose location
| LXC | Server        | Locatie                 |
|-----|---------------|-------------------------|
| 100 | Immich        | /opt/immich             |
| 102 | Media         | /srv/media              |
| 110 | Nextcloud     | Geen docker             |
| 121 | Vikunja       | /data/knowledge/vikunja |
| 122 | uMaps         | /opt/umap               |
| 150 | Preventie     | /srv                    |
| TBC | HomeAssistant | TBC                     |
