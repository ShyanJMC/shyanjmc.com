---
title: "GNU Linux - Internal System"
date: 2021-07-12
draft: false
weight: 2
---
# System Init

In an operative system, the system init (aka; sysinit) is the first program after the kernel start.

The sysinit\'s responsability is start the programs in the right order to make computer usable by the user.

In Linux systems have their sysinit at; /sbin/init. If the kernel do not have specified the path (place) in which load the sysinit, will load by default in; /sbin/init.

## History
At the beggining of portable systems (the operative system; Unix) there was a program with sysinit\'s responsabilities; sysvinit ("System V" by the AT&T Unix release and "Init"). AT&T Unix System V was released in 1983 and introduced "sysvinit". 

Sysvinit introduce in Unix systems new things;

* The concept of "daemon" and "service"; a program which start in system\'s boot.
* In "/etc/init.d" folder are the files in which sysvinit reads the daemon\'s configurations (the commands to start, restart, stop and check process).
* The "/etc/inittab" file is the system startup configuration.

Sysvinit devides the startup process in "runlevels".
A runlevel is a daemon/service group in which is started in a specific order. In Unix, the runlevels are available from 0 (zero) to 6 (six) and not startup one after another (runlevel 1 will not start after runlevel 0). Each runlevel functions depends of the distribution and configuration.

The runlevels standards are;

* 0 -> turnoff/shutdown.
* 1 -> single user mode (root), without graphical interface and network.
* 6 -> reboot.

The rest of runlevels are not standard but generally do this;

* 2,3,4 -> multi user and network without graphical interface.
* 5 -> multi user with graphical interface.

At today some linux distributions like Slackware still use sysvinit.

The main commands are;
- To change runlevel:
```bash
init [0-6]
```
- To manage services:
```bash
service [service_name] [start,stop,restart,reload,condrestart,status,--list,--add]
```
- To check system\'s boot process:
```bash
chkconfig [service_name]
```
```bash
chkconfig --list
```
- To enable or disable service startup:
```bash
chkconfig [service_name] [on,off]
```
## Evolutions
### Upstart
At 2006, Canonical (the company behind Ubuntu Linux), with the work of Scott James Remnant, relased a new sysinit; Upstart.

Upstart is a event-based sysinit. Event-based is a paradigm in which the software response to actions (system's or user's actions), input information, a message or information from another specific program, hardware actions, etc. The last official commit (changes in the code) was in 2014 and is under maintenance mode since 2016.

From [Wikipedia](https://en.wikipedia.org/wiki/Upstart_(software));

``Upstart operates asynchronously; it handles starting of the tasks and services during boot and stopping them during shutdown, and also supervises the tasks and services while the system is running. ``

At today Chrome/Chromium OS (from Google) use upstart.

The main commands are;
- Check configuration syntax:
```bash
init-checkconf -d /etc/init/process_name.conf
```
- To manage services:
```bash
[start,stop,restart] [job/service_name]
```
- To check system\'s boot process:
```bash
initctl list
```
- Show environment variables:
```bash
initctl list-env
```
- Set/Unset environment:
```bash
initctl [set,unset]-env foo=bar
```
- Reload configuration:
```bash
initctl reload-configuration
```
- Show relations and dependencies:
```bash
initctl2dot
```

Configurations files are in;
```bash
/etc/init/[service_name].conf
```

Services\' Information are in;
```bash
/var/log/upstart/[service,job].log
```

### Systemd
In 2011, RedHat developpers Lennart Poettering and Kay Sievers made Systemd with the idea of enhance Sysvinit and Upstart sysinits. The main idea was replace the computational overhead of shell, this is because those sysinits (Sysvinit and Upstart) use shell scripts to start,restart,stop and monitor status. Systemd introduced many new things;

* Units; like object oriented programming, units services can have states, own configurations, own environments, dependencies (others units, services or events).
* Parallel start: Systemd using units, can start services in parallel at the same time and enhance the boot speed.
* The complete change of paradigm; now Systemd absorved many others basic programs like logind, udevd, and others. And most of the community hate it, because breaks with the Unix philosofy; \"Do one thing per program, but do it well.\".

Now with systemd, you have a very complete sysinit and system manager in your linux. Systemd can manage without external help;
* Networking; DNS (systemd-resolved) and network interfaces (systemd-networkd).
* Containers; Something like the next evolution of chroot (systemd-nspawn).
* Syslog; journal as replacement of syslog.
* Mount points; systemd.mount as replacement of fstab.
* Boot; UEFI control (systemd-boot) and first boot (systemd-firstboot).
* Time Sync; systemd-timesyncd as replacement of ntpd and others.
* User control; User's home control (systemd-homed) and User's session control (systemd-logind).

And many many many others. But, what about if you want change systemd behavior for external program? Well, you can't. Systemd will stop self module for that task and will the leave control to that external program, but will be using CPU power and some RAM memory. Examples about it are; NetworkManager with systemd-networkd and systemd-resolved.

With this, the most of control about the Linux system is under systemd. Because of that there are many communities that do not like systemd (communities of Devuan, Artix, Gentoo, Slackware and others Linux distributions). Systemd is not bad itself, is just not modular as must be, because of that those communities created alternatives.

At 2021 the mayority of Linux distributions use Systemd as sysinit and system manager; Debian since 2019, Ubuntu since 15.04 version, Arch linux since 2012/3.

- Definitions
   * Service: is a program running at the boot init process.

The configurations files can be under;
```bash
/lib/systemd/[system,user]
/etc/systemd/[system,user]
```

The main commands are;

- Reload services configurations file:
```bash
systemctl daemon-reload
```

- Start, stop, reload service properly:
```bash
systemctl [service].service [start,stop,reload]
```

- See services's logs:
```bash
systemctl status -l [service].service
```

- If you want see service's configuration file:
```bash
systemctl cat [service].service
```

### OpenRC
Since 2007 Roy Marples (who sadly have cancer, good luck my friend) developped for 3 years the OpenRC system init. Since 2010 is maintained by Gentoo project and colaborators. OpenRC works
