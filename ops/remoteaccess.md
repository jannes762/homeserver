#centralhub.dev — External Access via Cloudflare Tunnel
## Doel
Veilige, browser-only toegang tot zelfgehoste services (Immich, Paperless, …)
zonder:
- VPN
- open poorten
- publiek IP
Geschikt voor netwerken waar VPN/software niet toegelaten is (bv. werk).

## Architectuur (high level)
```markdown
Browser (werk / extern)
   ↓ HTTPS (.dev, HSTS)
Cloudflare (DNS + Tunnel ingress)
   ↓ outbound-only tunnel
cloudflared (Proxmox host)
   ↓ LAN
LXC containers (Immich, Paperless, …)
```

## Belangrijk:
- Geen port forwarding
- Alle verbindingen zijn versleuteld
- Services zijn nooit direct internet-facing

##Domein & DNS
- Domein: centralhub.dev
- DNS beheer: Cloudflare
- .dev vereist HTTPS (HSTS preload) → automatisch afgedekt door Cloudflare
- DNS records worden niet manueel aangemaakt, maar via:
- `cloudflared tunnel route dns centralhub <hostname>`

## Cloudflare Tunnel
- Naam: centralhub
- Tunnel ID: e1c3e2a3-4b23-4094-8645-d0ace8241dfd
- Draait op: Proxmox host
- Installatie via package manager
- Start als systemd service
- Service status check
```bash
systemctl status cloudflared
journalctl -u cloudflared -n 100
```
Tunnel is correct actief wanneer logs bevatten:
Registered tunnel connection

## Configuratie
- Config file: `/etc/cloudflared/config.yml`
- Credentials: `/etc/cloudflared/e1c3e2a3-4b23-4094-8645-d0ace8241dfd.json`
   Rechten: `chmod 600 /etc/cloudflared/*.json`
- Een foutieve URL (bv. port-van-nextcloud) laat de hele tunnel crashen.

## Known pitfalls / lessons learned
Cloudflared service install faalt vaak door:
- fout pad naar credentials
- fout in config.yml
- placeholder URL’s
- dig is geen betrouwbare test bij proxied records
- Browser test is leidend

# Checklist: nieuwe service toevoegen aan centralhub.dev
1 Service bestaat en werkt intern
  - Service draait in LXC/VM
  - `pct exec <CTID> -- ip -br a`
  - `curl -I http://<IP>:<PORT>`
2 Subdomein kiezen
- 1 service = 1 subdomein
- Geen wildcards

3️ DNS-route toevoegen (Cloudflare Tunnel)
```bash
cloudflared tunnel route dns centralhub nextcloud.centralhub.dev
```

4 cloudflared config uitbreiden
In `/etc/cloudflared/config.yml`:
```bash
- hostname: nextcloud.centralhub.dev
  service: http://<IP>:<PORT>
```

5 Tunnel herstarten
```bash
systemctl restart cloudflared
systemctl status cloudflared --no-pager -l
```

Zoek naar:
```bash
Active: active (running)
Registered tunnel connection
```

6️ Extern testen (zonder VPN)
https://nextcloud.centralhub.dev

7 Toevoegen aan access policy
