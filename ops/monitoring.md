# Monitoring

## Scope

This document describes basic monitoring for system health and data integrity.
Monitoring is kept intentionally simple.

## Monitoring goals

- Detect disk failures early
- Detect ZFS issues
- Be aware of resource exhaustion
- Avoid alert fatigue

## ZFS monitoring

- Monthly scrubs scheduled
- Scrub results reviewed manually
- SMART monitoring enabled for all disks

Key indicators:
- Read/write errors
- Checksum errors
- Scrub failures

## Disk health

- SMART short tests periodically
- SMART long tests when anomalies appear
- Failed disks replaced proactively

## System resources

- CPU usage
- Memory usage
- Disk space usage

Monitored via:
- Proxmox dashboard
- Periodic manual checks

## Backup monitoring

- Borg backup logs reviewed regularly
- Periodic test restores performed
- Backup success is more important than backup speed

## Alerts

- No automated alerting initially
- Manual review preferred
- Alerts may be added later if complexity increases

## Rationale

This homelab is not mission-critical infrastructure.
Monitoring aims to prevent silent failures, not to provide real-time analytics.
