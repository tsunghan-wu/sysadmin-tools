# systemd

- Basic in Linux Operating system (run as PID 1)
- Unit files are in `/etc/systemd/system/` (which may be a symlink)

## System states

```
systemctl list-units    # list all units on the OS
systemctl --failed      # list all failed units
```

## Manage the units

```
systemctl status <unit name>                    # see unit status
systemctl help <unit name>
systemctl start/stop <unit name>
systemctl restart/reload <unit name>            # reload unit : only configurations
systemctl enable/disable <unit name>            # on boot or not
systemctl is-enable/is-active <unit name>       # check unit setting
systemctl daemon-reload                         # reload the systemd
```
 
## Write a system unit

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

- Reference
    - [Arch wiki](https://wiki.archlinux.org/index.php/Systemd)
