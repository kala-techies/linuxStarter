
# Day 07 — Advanced Commands and Troubleshooting (Examples)

This file contains practical examples and explanations for `grep`, `sed`, `awk`, troubleshooting tools (`dmesg`, `ss`/`netstat`, `tail`) and package management with `apt`/`yum`.

## Example 1 — Find recent errors in logs with grep

Goal: Find occurrences of the word "error" in `/var/log` and see file/line context.

Command:
```bash
grep -Rin "error" /var/log | head -n 50
```

Explanation:
- `-R` searches recursively, `-i` ignores case, `-n` shows line numbers. Piping to `head` limits output.
- If you need context around each match, add `-C 3` to show 3 lines before and after the match:
```bash
grep -RinC 3 "error" /var/log | less
```

## Example 2 — Replace text safely with sed

Goal: Replace all occurrences of `http://` with `https://` in a config file, but keep a backup.

Command:
```bash
sed -i.bak 's|http://|https://|g' /etc/myapp/config.conf
```

Explanation:
- `-i.bak` edits the file in-place and saves the original as `config.conf.bak`.
- Use `|` as delimiter if the pattern contains `/` to avoid escaping.

## Example 3 — Extract columns with awk

Goal: From `/etc/passwd`, print username and home directory for users with UID >= 1000.

Command:
```bash
awk -F":" '$3 >= 1000 {print $1, $6}' /etc/passwd
```

Explanation:
- `-F":"` sets `:` as the field separator. `$3` is the UID field. This helps list regular user accounts and their home paths.

## Example 4 — Investigate kernel messages for hardware errors

Goal: Look for disk-related errors reported by the kernel.

Command:
```bash
sudo dmesg | egrep -i "error|fail|I/O|ata|disk|sda"
```

Explanation:
- Kernel messages often indicate hardware problems early. Use `dmesg` and filter terms to find relevant warnings/errors.

## Example 5 — Find which process is using a port

Goal: Determine the process listening on port 3306 (MySQL default).

Command:
```bash
sudo ss -tulpn | grep :3306
```

Explanation:
- `ss -tulpn` shows TCP/UDP listening sockets with PID/program name. If nothing appears, the service may be down or bound to localhost only.

## Example 6 — Follow logs during troubleshooting

Goal: Watch system logs in real time while reproducing an issue.

Command:
```bash
sudo tail -n 200 -f /var/log/syslog
```

Explanation:
- `-n 200` shows the last 200 lines, `-f` follows new lines. Useful during deployments or when reproducing errors.

## Example 7 — Update and install a package (apt)

Goal: Update package lists, upgrade safely, then install `nginx`.

Commands:
```bash
sudo apt update
sudo apt upgrade -y
sudo apt install -y nginx
```

Explanation:
- `apt update` refreshes package lists. `apt upgrade` patches installed packages. `apt install` installs the requested package.

## Example 8 — Update and install a package (yum/dnf)

Goal: Similar workflow for RHEL/CentOS/Fedora systems.

Commands:
```bash
sudo yum update -y          # or: sudo dnf upgrade -y
sudo yum install -y nginx   # or: sudo dnf install -y nginx
```

Explanation:
- Use the distro's package manager. On newer Fedora systems `dnf` replaces `yum`.

## Example 9 — Safe in-place edits and rollbacks

Tip:
- When making bulk edits with `sed -i`, keep backups (`-i.bak`) and test the command with no `-i` first to verify changes.
- Use version control (git) for configuration directories when possible (e.g., `/etc` under a git-managed tree in a controlled workflow).

## Example 10 — Troubleshooting flow (quick checklist)

1. Check system and kernel messages:
	```bash
	sudo dmesg | tail -n 50
	sudo journalctl -b -p err --no-pager | tail -n 100
	```
2. Check listening ports / network issues:
	```bash
	ss -tuln
	sudo ss -tupn | grep <port>
	```
3. Search logs for error patterns:
	```bash
	grep -Rin "error\|warn\|fail" /var/log | head -n 200
	```
4. If a package/service is involved, check package manager logs and service logs and consider reinstalling/updating:
	```bash
	sudo apt install --reinstall problematic-package
	sudo systemctl restart problematic-service
	```

---

