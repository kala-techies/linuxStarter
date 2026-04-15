
# Day 06 — Scheduling and Automation (Examples)

Below are practical, step-by-step examples demonstrating how to schedule and manage tasks using `cron`, `at`, `watch`, and `systemctl`.

## Example 1 — Schedule a daily backup with cron

Goal: Run `/usr/local/bin/backup.sh` every day at 03:30 and keep stdout/stderr in a log.

Steps:
1. Open your crontab for editing:
```bash
crontab -e
```
2. Add this line to the crontab:
```cron
30 3 * * * /usr/local/bin/backup.sh >> /var/log/backup.log 2>&1
```
3. Save and exit. Verify the entry:
```bash
crontab -l
```

Notes:
- Use the full path to the script and log file. Cron runs with a minimal PATH.
- Redirect both stdout and stderr so you can inspect failures in `/var/log/backup.log`.

## Example 2 — Run a one-time job with at

Goal: Schedule a database maintenance command to run tomorrow at 02:00.

Steps:
```bash
echo "/usr/local/bin/db-maintenance.sh >> /var/log/db-maint.log 2>&1" | at 02:00 tomorrow
atq    # verify the scheduled job appears
```

To cancel:
```bash
atrm <jobnumber>
```

Notes:
- `at` is for one-off tasks. `cron` is better for repeating schedules.

## Example 3 — Monitor a log directory with watch

Goal: Watch top 10 largest files in `/var/log` every 5 seconds.

Command:
```bash
watch -n 5 "du -sh /var/log/* 2>/dev/null | sort -hr | head -n 10"
```

Explanation:
- `watch` runs the command every 5 seconds and updates the display. Useful during troubleshooting or log growth investigations.

## Example 4 — Manage service start at boot with systemctl

Goal: Ensure `nginx` starts on boot, start it now, and check status.

Commands:
```bash
sudo systemctl enable nginx.service    # enable at boot
sudo systemctl start nginx.service     # start now
systemctl status nginx.service         # view status (no sudo needed to view)
sudo journalctl -u nginx.service -n 100 --no-pager   # check recent logs
```

Notes:
- If the service fails to start, check `journalctl` for errors. Use `sudo systemctl restart nginx.service` after fixing configuration.

## Example 5 — Use cron's @reboot and testing locally

Goal: Run a small script at system boot using `@reboot` (useful for simple startups).

Crontab entry:
```cron
@reboot /usr/local/bin/start-helper.sh >> /var/log/start-helper.log 2>&1
```

Testing tip:
- To test an `@reboot` job without rebooting, run the command manually or simulate environment by executing the script as the targeted user.

## Example 6 — Best practices and troubleshooting

- Always use absolute paths in cron/at entries.
- Add a small header to cron jobs to set environment variables if needed, e.g.:
```cron
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
```
- If a cron job doesn't run, inspect `/var/log/cron` (or `journalctl` on systemd systems) and check the user's mail (cron may email stderr to the user).

---

