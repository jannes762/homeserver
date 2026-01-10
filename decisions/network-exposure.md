# Network exposure strategy

## Goals

- Minimize attack surface
- Avoid direct internet exposure of services
- Prefer encrypted access paths

## Current setup

- Static public IP
- ISP router (Telenet)
- Port forwarding available but discouraged

## Preferred access method

- VPN (WireGuard)
- Services accessible only through VPN

## Exceptions

Port forwarding may be used temporarily for:
- Initial testing
- Services that explicitly require public access

Such exposure should be documented and reviewed.

## Domain usage

- No domain name currently
- Domain may be added later for convenience
- Domain does not change exposure strategy

## Rationale

Reducing exposed services significantly lowers security risks.
Convenience is secondary to safety.


# VPN Externe Toegang

## Doel
Veilige toegang tot home server, Immich, Bitwarden, etc.

## Opties
- WireGuard (aangeraden)
- Tailscale (optioneel)

## Setup WireGuard
1. Server:
   - Installatie WireGuard
   - Genereer keys
   - Config peer(s) (laptop, smartphone)
2. Client:
   - Android/iOS: WireGuard app
   - Split-tunnel optie aan (alleen apps via VPN)

## Router / ISP
- Dynamic DNS of vast IP
- Poorten open niet strikt nodig (WireGuard kan out-of-the-box)
- Zorg dat VPN start met server

## Tips
- Test verbinding lokaal eerst
- Daarna extern
- Split-tunnel voorkomt dat al je internet via server gaat