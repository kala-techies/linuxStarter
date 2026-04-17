# linuxStarter — 7-Day Quick Cheat Sheet

This single-page cheat sheet collects the most useful, frequently-used commands from Day 1 to Day 7. Keep the per-day `commands.md` and `examples.md` for learning and context — this file is a compact reference for quick lookups.

## Day 1–2: Basics & Files
- ls, pwd, cd, mkdir, rmdir, touch, rm, cp, mv, ln
- find . -name pattern
- file filename
- tree (install: sudo apt install tree)

## Day 3: Permissions & Ownership
- chmod 644 file.txt  # set numeric perms
- chmod +x script.sh  # make executable
- chown user:group file
- umask (check or set default permissions)

## Day 4: Users & Processes
- sudo useradd -m -s /bin/bash username
- sudo usermod -aG docker username
- sudo userdel -r username
- ps aux | less
- top / htop
- sudo kill <pid> && sudo kill -9 <pid>

## Day 5: Networking & Monitoring
- ip addr show / ip route show
- ping -c 4 host
- ss -tuln (listening sockets)
- curl -I https://example.com
- df -h, du -sh /path
- free -h, uptime, vmstat

## Day 6: Scheduling & Automation
- crontab -e  # edit cron
- crontab -l
- cron entry: 30 3 * * * /path/script.sh >> /var/log/job.log 2>&1
- echo "cmd" | at 09:30
- watch -n 2 'df -h'
- systemctl start|stop|restart|enable service

## Day 7: Advanced & Troubleshooting
- grep -Rin "pattern" /path
- sed -i.bak 's/old/new/g' file
- awk -F":" '{print $1,$6}' /etc/passwd
- sudo dmesg | tail -n 50
- ss -tulpn | grep :8080
- sudo apt update && sudo apt upgrade -y

## Quick safety reminders
- Always use absolute paths and redirect logs in cron/at jobs.
- Prefer `kill` (SIGTERM) before `kill -9` (SIGKILL).
- Use `-i.bak` or test `sed` without `-i` before applying in-place edits.
- Use `sudo` only when needed and test in non-production first.

---

## Final note

This cheat sheet collects the most frequently used commands and the core knowledge you should be familiar with. Don't let this list be a limit — use it as a quick reference while you practice the full examples in each day's `examples.md`.

If you want to go further, continue working on the topics below to gain mastery: dig into advanced options, build small projects that use these tools, and study system-specific details (systemd, networking stacks, security hardening, shell scripting, etc.). Keep learning and experimenting — this sheet is a starting point, not the finish line.

## How to explore these topics (practical steps)

If you're not sure how to continue, follow these concrete steps to learn effectively:

1. Hands-on in a safe environment
   - Create a disposable VM or container (Docker) to practise. Example:
     ```bash
     docker run -it --rm ubuntu:22.04 bash
     apt update && apt install -y iproute2 procps curl vim less
     ```
   - Use the container to try commands from each day's `examples.md` without risking your host system.

2. Follow the examples, then modify them
   - Run the example exactly once, then change parameters (paths, flags) to see different outputs. Keep notes of what changed.

3. Build tiny projects per day
   - Day 1–2: create a sample project structure and write a small script to deploy it.
   - Day 3: create a group and set shared permissions for a folder.
   - Day 4: add a test user in a container and inspect processes while running a simple service.
   - Day 5: capture `ip addr`, `ss`, and `curl` outputs and save them for analysis.
   - Day 6: schedule a cron job that writes a timestamp to a file every minute (in a container) and observe logs.
   - Day 7: write `sed`/`awk` one-liners to transform a CSV file.

4. Read and use authoritative docs
   - `man` pages: `man grep`, `man sed`, `man awk`, `man crontab`, `man systemctl`.
   - TLDR pages and explainshell (https://explainshell.com/) for quick explanations.

5. Practice with small challenges
   - Use interactive labs (Katacoda, Codecademy, OverTheWire for security-focused practice).
   - Give yourself short tasks (e.g., "find the 5 largest files in /var/log and report them") and time yourself.

6. Automate and version-control your practice
   - Keep scripts and sample configs in a git repo. Commit changes so you can roll back and track learning.

7. Ask and research
   - When stuck, search error messages, read related man pages, and ask on forums (Stack Overflow, Server Fault) with clear reproduction steps.

8. Repeat and expand
   - Once comfortable, combine topics (e.g., cron + logging + systemctl) to create small real-world workflows.

---

## Thanks

Thanks to everyone who believed in me and took the time to go through this content — your support means a lot. If this material helped, please share feedback or improvements.

Thanks for reading — Kalandar