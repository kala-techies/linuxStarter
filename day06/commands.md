# Day 06 — Scheduling and Automation (Commands)

This file provides concise command references for scheduling and automating tasks: cron, at, watch, and basic `systemctl` service control.

## cron / crontab

- Edit the current user's crontab (interactive editor):
```bash
crontab -e
```

- List the current user's crontab entries:
```bash
crontab -l
```

- Remove the current user's crontab:
```bash
crontab -r
```

- Cron time fields format (minute hour day month weekday) — examples:
```cron
# run at 2:30 AM every day
30 2 * * * /path/to/script.sh

# run every 15 minutes
*/15 * * * * /path/to/script.sh

# run at reboot (some systems support @reboot)
@reboot /path/to/startup-script.sh
```

## at / batch / atrm / atq

- Schedule a one-time job at specific time:
```bash
echo "/path/to/command arg1" | at 09:30
```
Or interactively:
```bash
at 09:30
# then type the commands followed by Ctrl+D
```

- List pending `at` jobs:
```bash
atq
```

- Remove a pending `at` job (by job number):
```bash
atrm <jobnumber>
```

- `batch` runs jobs when system load is low:
```bash
echo "/path/to/command" | batch
```

## watch

- Run a command repeatedly and watch output change:
```bash
watch -n 2 'df -h'
```
Options:
	- `-n <seconds>` — interval in seconds (default 2s).
	- `-d` — highlight differences between updates.

## systemctl (systemd)

- Check service status:
```bash
systemctl status nginx.service
```

- Start / stop / restart a service:
```bash
sudo systemctl start nginx.service
sudo systemctl stop nginx.service
sudo systemctl restart nginx.service
```

- Enable service at boot / disable:
```bash
sudo systemctl enable nginx.service
sudo systemctl disable nginx.service
```

- View logs for a service (journalctl):
```bash
sudo journalctl -u nginx.service -n 200 --no-pager
```

## Tips & quick references

- Cron environment: Cron jobs run with a limited environment (minimal PATH). Use full paths or set PATH in the crontab.
- Use absolute paths for scripts and redirect stdout/stderr to logs in cron entries, e.g.: `/path/script.sh >> /var/log/myscript.log 2>&1`.
- Use `systemctl` for long-running services; use `cron`/`at` for scheduled tasks.

