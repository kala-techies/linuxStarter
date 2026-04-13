
# Day 04 — Filesystem Navigation and File Operations

This file lists common Linux filesystem and navigation commands with a few practical examples and short safety notes.

## Directory management

- Create a directory:
```bash
mkdir directory_name
```
# Day 04 — User Management and Process Management

This document covers common commands for adding/removing/modifying users and groups, plus basic process management (viewing, controlling, and inspecting processes). Examples include safe usages and short notes about system files and permissions.

## Requirements / scope

- Add, modify, and remove users: `useradd`, `adduser` (Debian-friendly), `usermod`, `userdel`, `passwd`.
- Manage groups: `groupadd`, `groupdel`, `groups`, `id`, `gpasswd`, `usermod -aG`.
- Process inspection and control: `ps`, `top`, `htop`, `pgrep`, `pkill`, `kill`, `kill -9`, `nice`, `renice`, job control (`&`, `jobs`, `fg`, `bg`).

> Many user/group commands require root. Use `sudo` when appropriate.

## User management

- Add a new user (create home directory and set shell):
```bash
sudo useradd -m -s /bin/bash -c "Full Name" -G sudo username
```
Notes:
	- `-m` creates a home directory (/home/username).
	- `-s` sets login shell.
	- `-G` sets supplementary groups (comma-separated).

- Debian/Ubuntu friendly (interactive):
```bash
sudo adduser username
```

- Set or change a user's password:
```bash
sudo passwd username
```

- Modify an existing user (e.g., add to a group):
```bash
sudo usermod -aG docker username   # add to 'docker' group
sudo usermod -c "New Comment" -l newlogin oldlogin  # change comment/login
```

- Delete a user (keep/remove home):
```bash
sudo userdel username        # leaves home
sudo userdel -r username     # removes home and mail spool
```

- Lock and unlock an account:
```bash
sudo passwd -l username  # lock
sudo passwd -u username  # unlock
```

- Inspect user and account info:
```bash
getent passwd username   # shows passwd entry from NSS
id username              # uid/gid and group membership
groups username
sudo chage -l username   # password expiry info
```

## Group management

- Create and remove groups:
```bash
sudo groupadd devs
sudo groupdel oldgroup
```

- View groups for the current user:
```bash
groups
id
```

## Important system files

- /etc/passwd — user account info (non-secret fields)
- /etc/shadow — password hashes and expiry (root-readable only)
- /etc/group — group membership

Use `getent passwd`/`getent group` to query the system using NSS (works with LDAP/NIS, etc.).

## Process management — viewing processes

- List processes (BSD format):
```bash
ps aux | less
```

- List processes (Unix style):
```bash
ps -ef | less
```

- Find a process by name/PID:
```bash
pgrep -l sshd      # show PIDs and names
ps -p <pid> -o pid,ppid,cmd,%mem,%cpu
```

- Interactive viewers:
```bash
top               # built-in, interactive
htop              # nicer UI (install: sudo apt install htop)
```

## Process control — stopping/killing

- Graceful termination (ask process to exit):
```bash
sudo kill <pid>    # sends SIGTERM (15)
```

- Forceful termination (use only when necessary):
```bash
sudo kill -9 <pid> # sends SIGKILL (9)
```
Note: SIGTERM lets the process clean up; prefer it before SIGKILL.

- Kill by name:
```bash
sudo pkill -f process_name   # matches full command line
sudo killall process_name    # kill by executable name (not on all distros)
```

## Jobs, background and foreground

- Start a command in background:
```bash
sleep 600 &
```

- List jobs in current shell:
```bash
jobs -l
```

- Bring a job to foreground or background:
```bash
fg %1
bg %1
```

## Priorities: nice and renice

- Start a process with a lower priority (higher niceness number):
```bash
nice -n 10 long_running_command
```

- Change priority of running process:
```bash
sudo renice -n 5 -p <pid>
```

## Service management (brief)

- Many user-space daemons are managed by systemd. View status and control services:
```bash
sudo systemctl status sshd.service
sudo systemctl start|stop|restart|enable|disable sshd.service
```

## Examples / real-life tasks

- Add developer user and set password:
```bash
sudo useradd -m -s /bin/bash -G sudo -c "Dev User" devuser
sudo passwd devuser
```

- Add existing user to the `docker` group so they can run Docker without sudo:
```bash
sudo usermod -aG docker alice
```

- Find and kill a runaway process:
```bash
pgrep -f myscript.py     # find PID(s)
sudo kill <pid>           # try graceful
sudo kill -9 <pid>        # if that fails
```

## Safety notes

- Always prefer `kill` (SIGTERM) before `kill -9` (SIGKILL).
- Use `userdel -r` with caution (it removes home and mail spools).
- Operations that modify users/groups usually require root. Test on a non-production system when possible.

## Further reading

- `man useradd`, `man usermod`, `man userdel`, `man passwd`, `man ps`, `man kill`, `man systemctl`.

---
