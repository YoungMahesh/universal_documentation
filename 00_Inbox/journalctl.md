systemd includes a logging system called **journald**

You can inspect logs using `journalctl`.

```sh
# all logs
journalctl

# logs from current boot
journalctl -b

# logs from previous boot
journalctl -b -1

# logs of a particular service
journalctl -u nginx

# follow logs in real time
journalctl -f

# user service logs
journalctl --user -u hyprsunset
```

This is particularly useful when a service fails to start.
