
# Day 07 — Advanced Commands and Troubleshooting (Commands)

This file lists advanced file-manipulation utilities (`sed`, `grep`, `awk`), troubleshooting tools (`dmesg`, `netstat`/`ss`, `tail`), and common package-management commands for `apt` and `yum`.

## grep (search)

- Search for a string in files (recursive):
```bash
grep -R "search_text" /var/log
```

- Case-insensitive search, show line numbers:
```bash
grep -in "error" /var/log/syslog
```

- Show matching filenames only:
```bash
grep -l "TODO" *.py
```

- Use ripgrep (`rg`) if available for faster recursive searches.

## sed (stream editor)

- Substitute first occurrence on each line (print to stdout):
```bash
sed 's/old/new/' file.txt
```

- Global substitution on each line:
```bash
sed 's/old/new/g' file.txt
```

- In-place edit (GNU sed):
```bash
sed -i 's/old/new/g' file.txt
```

- Delete lines matching a pattern:
```bash
sed -i '/^#/d' file.txt   # remove comment lines
```

## awk (text processing / column extraction)

- Print the 1st and 3rd columns (space-separated):
```bash
awk '{print $1, $3}' file.txt
```

- Sum values in column 2:
```bash
awk '{sum += $2} END {print sum}' file.txt
```

- Use field separator (CSV):
```bash
awk -F"," '{print $2}' file.csv
```

## dmesg and kernel messages

- Display kernel ring buffer:
```bash
dmesg | less
```

- Show new messages interactively (requires root to see all):
```bash
sudo dmesg --follow
```

## netstat / ss (network sockets)

- Modern: show listening TCP/UDP ports:
```bash
ss -tuln
```

- Older `netstat` equivalent:
```bash
netstat -tuln
```

- Show connections with process names (may require sudo):
```bash
ss -tupn
```

## tail and log inspection

- Tail last N lines:
```bash
tail -n 200 /var/log/syslog
```

- Follow file in real time:
```bash
tail -f /var/log/syslog
```

- Use `multitail` or `less +F` for more advanced viewing.

## apt (Debian/Ubuntu) package management

- Update package lists and upgrade installed packages:
```bash
sudo apt update
sudo apt upgrade -y
```

- Install / remove a package:
```bash
sudo apt install -y package_name
sudo apt remove -y package_name
```

- Search for a package:
```bash
apt search package_keyword
```

## yum / dnf (RHEL/CentOS/Fedora)

- Update packages:
```bash
sudo yum update        # or: sudo dnf upgrade
```

- Install / remove a package:
```bash
sudo yum install -y package_name   # or: sudo dnf install -y package_name
sudo yum remove -y package_name
```

## Quick troubleshooting combos

- Find recent kernel errors and filter for disk/usb:
```bash
sudo dmesg | egrep -i "error|fail|disk|usb"
```

- Find which process holds a TCP port (e.g., 8080):
```bash
ss -tulpn | grep :8080
```

- Search logs for an error and print surrounding lines:
```bash
grep -in "segfault" /var/log/* | while read -r line; do echo "$line"; done
grep -R -n "Exception" /var/log | xargs -r -n1 -I{} sed -n -e "{}"p
```

## Notes

- Prefer `ss` over `netstat` on newer systems. Many commands require root (`sudo`) to see full details.
- When using `sed -i`, consider creating a backup with `-i.bak` when editing important files.

