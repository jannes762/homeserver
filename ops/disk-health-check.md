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