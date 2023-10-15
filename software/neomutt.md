# Neomutt

- Use `a` to add a new contact to `abook`
- Use `<CTRL+t>` to change the filetype of your email. You can change it to plain text or html.

## Calling mbsync automatically

Follow the instructions available in the [arch
wiki:](https://wiki.archlinux.org/title/Isync)

### With a timer

If you want to automatically synchronize your mailboxes, start `isync`
automatically with a `systemd/User` unit. The following service file can start
the `mbsync` command:

`~/.config/systemd/user/mbsync.service`

```
[Unit]
Description=Mailbox synchronization service

[Service]
Type=oneshot
ExecStart=/usr/bin/mbsync -Va

[Install]
WantedBy=default.target
```

The following timer configures `mbsync` to start 2 minutes after boot, and then
every 5 minutes:

`~/.config/systemd/user/mbsync.timer`

```
[Unit]
Description=Mailbox synchronization timer

[Timer]
OnBootSec=2m
OnUnitActiveSec=5m
Unit=mbsync.service

[Install]
WantedBy=timers.target
```

After creating the files, `reload` `systemd`, then `enable` and `start`
`mbsync.timer`, adding the `--user` flag to `systemctl`.

Note: The `mbsync` service now runs only after login. It's also possible to
launch the `systemd-user` instances after boot if you configure
`Systemd/User#Automatic` start-up of `systemd` user instances.
