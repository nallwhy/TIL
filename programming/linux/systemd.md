## Systemd

In recent years, Linux distributions have increasingly transitioned from other init systems to systemd. The systemd suite of tools provides a fast and flexible init model for managing an entire machine from boot onwards.

### Unit

`unit`: basic object
the most common type is a `service`

To manage services on a systemd enabled server, our main tool is the `systemctl` command.

```bash
$ sudo systemctl start nginx.service
$ sudo systemctl stop nginx.service
$ sudo systemctl restart nginx.service
$ sudo systemctl reload nginx.service
```

### Enableing or Disabling Units

To let systemd unit files start automatically at boot, you need to `enable` to unit. This hooks is up to a certain boot `target`, causing it to be triggered when that target is started.

```bash
# enable service
$ sudo systemctl enable nginx.service

# disable service
$ sudo systemctl disable nginx.service
```

### Log

`journald` collects and manages journal entries from the system.

To see all log entries:
```bash
$ journalctl
```

If you only wish to see the journal entries from the current boot, add the -b flag:
```bash
$ journalctl -b
```

To see only kernel messages, such as those that are typically represented by dmesg, you can use the -k flag:
```bash
$ journalctl -k
```

Combination
```bash
$ journalctl -k -b
```

To see all of the journal entries for the unit in question, give the -u option with the unit name to the journalctl command:
```bash
$ journalctl -u nginx.service
```

As always, you can limit the entries to the current boot by adding the -b flag:
```bash
$ journalctl -b -u nginx.service
```

To filter the log by time:
```bash
$ journalctl --since "2015-01-10" --until "1 hour ago"
```

#### Journal Maintenance

To check disk usage:
```bash
$ journalctl --disk-usage
```

To delete old logs:
```bash
# by size
$ sudo journalctl --vacuum-size=1G

# by time
$ sudo journalctl --vacuum-time=1years
```

#### Limiting Journal Expansion

`/etc/systemd/journald.conf`

* `SystemMaxUse=`: Specifies the maximum disk space that can be used by the journal in persistent storage.
* `SystemKeepFree=`: Specifies the amount of space that the journal should leave free when adding journal entries to persistent storage.
* `SystemMaxFileSize=`: Controls how large individual journal files can grow to in persistent storage before being rotated.
* `RuntimeMaxUse=`: Specifies the maximum disk space that can be used in volatile storage (within the /run filesystem).
* `RuntimeKeepFree=`: Specifies the amount of space to be set aside for other uses when writing data to volatile storage (within the /run filesystem).
* `RuntimeMaxFileSize=`: Specifies the amount of space that an individual journal file can take up in volatile storage (within the /run filesystem) before being rotated.

### Status

To check the status of a service on your system, you can use the status command:
```bash
$ systemctl status application.service
```

### Modifying Unit Files

To add a unit file snippet, which can be used to append or override settings in the default unit file, simply call the edit option on the unit:
```bash
$ sudo systemctl edit nginx.service
```

If you prefer to modify the entire content of the unit file instead of creating a snippet, pass the --full flag:
```bash
$ sudo systemctl edit --full nginx.service
```

After modifying a unit file, you should reload the systemd process itself to pick up your changes:
```bash
$ sudo systemctl daemon-reload
```

### Tagets (Runlevels)

Another function of an init system is to transition the server itself between different states. Traditional init systems typically refer to these as "runlevels", allowing the system to only be in one runlevel at any one time.

In systemd, "targets" are used instead. Targets are basically synchronization points that the server can used to bring the server into a specific state. Service and other unit files can be tied to a target and multiple targets can be active at the same time.

### Running Your Own Service

ex) Run erlang release and let it automatically run after boot.

#### Creating a Service

`/lib/systemd/system/myapp.service`
```
[Unit]
Description="Job that run the myapp app"

[Service]
Type=simple
Environment="HOME=/home/ubuntu"
Environment="PORT=80"
ExecStart=/home/ubuntu/apps/bin/myapp foreground
ExecStop=/home/ubuntu/apps/bin/myapp stop
ExecReload=/home/ubuntu/apps/bin/myapp reboot
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

#### Reloading daemons

```bash
$ sudo systemd daemon-reload
```

#### Starting a Service

```bash
$ sudo systemctl start myapp
```

#### Enabling a Service

```bash
$ sudo systemctl enable myapp
$ systemctl is-enabled myapp
enabled
```

Reference:  
https://www.digitalocean.com/community/tutorials/systemd-essentials-working-with-services-units-and-the-journal  
https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files  
https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs  
https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/chap-Managing_Services_with_systemd.html
