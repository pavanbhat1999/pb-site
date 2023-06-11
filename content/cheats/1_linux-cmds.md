+++
title = "Linux Commands"
date = 2022-01-04
+++

## Battery status
```bash
    cat /sys/class/power_supply/BAT0/status
    acpid
    sudo bat -t <limit_range>
 ```
## File Operations
```bash
    du -chd 1 | sort -h
    ls -l
```
## Burn ISO
```bash
    dd bs=4M if=/path/to/archlinux.iso of=/dev/sdx status=progress && sync
```
