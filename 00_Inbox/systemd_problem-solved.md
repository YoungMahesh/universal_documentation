systemd was created to solve problems with the traditional Linux startup and service-management system, particularly SysVinit.

Before systemd, most Linux distributions used SysVinit, which had been inherited from traditional Unix systems.

The fundamental problem was that Linux systems had become much more complex, but their service-management infrastructure was still based on an older, relatively simple design.

Before systemd, linux was booted like this:

1. BIOS/UEFI
2. Bootloader (GRUB)
3. Linux kernel
4. init (PID 1) - SysVinit
5. Runlevel scripts
6. System services (Networking, SSH, Cron, Display manager, etc)

SysVinit used shell scripts to start and stop services.

For example, services could have scripts such as:

```sh
/etc/init.d/ssh
/etc/init.d/cron
/etc/init.d/networking
```

The scripts were invoked according to runlevels and their startup ordering.

This approach worked, but several problems emerged.

### Problem 1: Slow boot process

Traditional init systems often started services sequencially

For example:
Start networking -> Wait for networking -> Start SSH -> Start cron -> Start display manager

Even when services were independent, startup scripts often introduced unnecessary waiting.

systemd introduced depedency-based paralled
service startup.

### Problem 2: Difficult depedency management

Suppose service A requires service B to be running.
With SysVinit, administrators often managed startup ordering using script names conventions such as:

```
S01networking
S02ssh
S03application
```

This was relatively inflexible.

systemd introduced explicit depedency relationships:

```ini
[Unit]
Description=My Application
After=network.target
Requires=some-service.service
```

It can construct dependency graph and determine which jobs can run concurrently.

### Problem 3: Poor process tracking

Traditional service scripts frequently relied on PID files to track processes.

This could cause problems when:

- A service spawned child processes
- A process crashed
- A service daemonized itself
- A service left behind orphaned processes

systemd uses Linux control groups (cgroups) to track processes belonging to a service.
This makes process of supervision and resource management more reliable

### Problem 4: Services started even when they weren't needed

Traditionally, many services were started
during boot whethere or not anything needed them immediately.

systemd introduced socket activation, D-Bus activation and other on-demand mechanisms.

For example, a service can be started when a client connects to its socket rather than being started immediately during boot.

### Problem 5: No unified management interface

Linux had separate tools and mechanism for managing different system resources:

- Services: init scripts
- Scheduled tasks: cron
- Device management: udev
- Mounting: mount/fstab
- Logging: syslog
- User sessions: separate session-management mechanisms

systemd gradually introduced a common management framework using different types of units

For example:

| Unit         | Purpose                         |
| ------------ | ------------------------------- |
| `.service`   | Manage services                 |
| `.socket`    | Socket activation               |
| `.timer`     | Scheduled tasks                 |
| `.mount`     | Mount filesystems               |
| `.automount` | Automatically mount filesystems |
| `.target`    | Group units into system states  |
| `.device`    | Represent devices               |
