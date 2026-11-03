```sh
# list user services
systemctl --user list-units --type=service

# list system services
systemctl list-units --type=service

# check user service status
systemctl --user status hyprsunset.service

# check service status
systemctl status hyprsunset.service

# start a service
sudo systemctl start hyprsunset.service

# stop a service
sudo systemctl stop hyprsunset.service

# restart a service
sudo systemctl restart hyprsunset.service

# reload service configuration
sudo systemctl reload hyprsunset.service

# enable a service at boot
sudo systemctl enable hyprsunset.service

# check whether is service is enabled
systemctl --user is-enabled hyprsunset.service

# disable automatic startup
sudo systemctl disable hyprsunset.service

# enable and start immediately
sudo systemctl enable --now hyprsunset.service

# stop and disable
sudo systemctl disable --now hyprsunset.service
```

systemd reads unit files from several directories.

| Location                   | Purpose                                           |
| -------------------------- | ------------------------------------------------- |
| `/usr/lib/systemd/system/` | System-installed services                         |
| `/etc/systemd/system`      | Adminstrator-created or overriden system services |
| `/usr/lib/systemd/user`    | System-installed user services                    |
| `~/.config/systemd/user/`  | Your personal user services                       |


---

Service creation example:

1. Create: `~/.config/systemd/user/myapp.service`

```service
[Unit]
Description=My Background application

[Service]
ExecStart=/usr/bin/sleep infinity
Restart=on-failure

[Install]
WantedBy=default.target
```

2. Reload systemd:
```sh
systemctl --user daemon-reload
```

3. Start it:
```sh
systemctl --user start myapp
```

4. Enable it at login:
```sh
systemctl --user enable myapp
```

5. Check its status:
```sh
systemctl --user status myapp
```

---

[Problem solved by sysetm](./systemd_problem-solved.md)

[History of systemd](./systemd_history.md)

[Logs of systemd](./journalctl.md)

systemd is the init system and service manager used by most modern Linux distributions including OmarchyOS.

It manages services, background processes, system startup, logs, timers, mounts, networking, and much more.

### How systemd works

When your Linux computer boots:

1. The Linux kernel initializes hardware.
2. The kernel starts the first [userspace](./userspace) process: `systemd` (PID 1).
3. systemd starts the services and processes required by your system.
4. Your login manager starts your graphical session.
5. Your desktop environment (Hyprland) starts.

Check whether systemd is running:

```sh
ps -p 1 -o pid,comm,args
```

Expected output:

```txt
PID  COMMAND  COMMAND
1    systemd  /sbin/init
```

### systemd units

Everything systemd manages is represented through a concept called a unit.

Common unit types:

| Unit         | Purpose                  |
| ------------ | ------------------------ |
| `.service`   | Background services      |
| `.timer`     | Scheduled tasks          |
| `.socket`    | Socket-based activation  |
| `.mount`     | Filesystem mounts        |
| `.automount` | Automatic mounting       |
| `.target`    | Groups of units          |
| `.path`      | Monitor filesystem paths |
| `.device`    | Device management        |
| `.slice`     | Resource management      |

### Managing services

An important distiction:

| Command         | Meaning                           |
| --------------- | --------------------------------- |
| `start`         | Start now                         |
| `stop`          | Stop now                          |
| `enable`        | Start automatically at boot       |
| `disable`       | Don't start automatically at boot |
| `enable --now`  | Enable and start now              |
| `disable --now` | Disable and stop now              |

### System services vs user services

systemd has two important management scopes.

---

**System manager**

```sh
sudo systemctl start nginx
```

- Runs system-wide.
- Usually manages services requiring root privileges.
- Starts during sytem boot.

---

**User manager**

```sh
systemctl --user start hyprsunset
```

- Runs under your individual user account.
- Manages applications and services belonging to that user.
- Commonly used for desktop applications.

For example, `hyprsunset` is appropriate as a user service because it belongs to your graphical session.

---

### Understanding targets

A target is a logical grouping of units.

For example:

| Target | Purpose |
|-|-|
| `multi-user.target` | Multi-user, non-graphical system |
| `graphical.target` | Graphical login environment |
| `default.target` | Default target for the relevant manager |
| `network-online.target` | Network is considered online |
| `basic.target` | Basic system initialization |

Target helps systemd organize startup dependencies.

For example:
```service
[Install]
WantedBy=graphical.target
```

This means the service should be started when the graphical target is reached, if enabled.

Inspect the default system target:
```sh
systemctl get-default
```
