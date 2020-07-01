# systemd

- Basic in Linux Operating system (run as PID 1)
- Unit files are in `/etc/systemd/system/` (which may be a symlink)

## A. Systemctl

> Commands that controls systemd

### System states

```
systemctl list-units    # list all units on the OS
systemctl --state=failed      # list all failed units
```

### Manage the units

```
systemctl status <unit name>                    # see unit status
systemctl help <unit name>
systemctl start/stop <unit name>
systemctl restart/reload <unit name>            # reload unit : only configurations
systemctl enable/disable <unit name>            # on boot or not
systemctl is-enable/is-active <unit name>       # check unit setting
systemctl daemon-reload                         # reload the systemd
```
 
### Write a system unit

> File path : `/etc/systemd/system/<unit name>.service`

```
[Unit]
Description=<description>
Requires=<hard dependancy>
Wants=<soft dependancy>
After=<the unit must start after ...>

[Service]
Type=<type>
ExecStart=<start command>
ExecStop=<stop command>
User=<>
Group=<>
WorkingDirectory=<>
Restart=always
RestartSec=30

[Install]
WantedBy=multi-user.target
```
## B. journalctl

> Commands that query systemd logs

### Format

```
journalctl _FIELD=VALUE --option
```

### Kernel Related

```
journalctl --list-boots         # list boot numbers for debugging
journalctl -b [ID][±offset]     # query specific boot
journalctl -k                   # show only kernel messages
# ex: journalctl -k -b -1 -> See all kernel logs from previous boot
```

### Time

```
journalctl --since="<year>-<month>-<day> xx:xx:xx"
journalctl --until="<year>-<month>-<day> xx:xx:xx"
```

### Query Unit

```
journalctl _SYSTEMD_UNIT=<unit name>.service
journalctl _PID=<pid>
```

### Options

```
journalctl -f           # Show live message
journalctl -o <output>  # Specify output format/path
journalctl-p <priority>
journalctl _SYSTEMD_UNIT=<A>.service + _SYSTEMD_UNIT=<B>.service    # OR operation
```

## C. Troubleshooting

1. `systemctl`
    - list failed
    - specific unit status -> get pid
2. `journalctl`
    - set correct boot-id
    - set correct unit, pid option
3. Debug
4. Restart process

- Reference
    - [Arch wiki](https://wiki.archlinux.org/index.php/Systemd)
    - Man Page

