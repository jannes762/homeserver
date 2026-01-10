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
