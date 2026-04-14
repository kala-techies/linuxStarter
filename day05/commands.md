# Day 05 — Networking and System Monitoring (Commands)

This file lists common networking and system-monitoring commands with concise examples and useful flags.

## Network discovery & interfaces

- Show network interfaces (modern):
```bash
ip addr show         # or: ip a
```

- Show routing table:
```bash
ip route show        # or: ip r
```

- Bring interface up/down:
```bash
sudo ip link set dev eth0 up
sudo ip link set dev eth0 down
```

- Legacy command (if installed):
```bash
ifconfig -a
```

## Basic network troubleshooting

- Test connectivity to a host:
```bash
ping -c 4 example.com
```

- Trace route to a host:
```bash
traceroute example.com    # may require sudo/install
```

- Show open sockets and listening ports:
```bash
ss -tuln       # modern replacement for netstat
netstat -tuln  # older systems
```

- Resolve DNS for a hostname:
```bash
dig example.com A    # if bind-utils/dnsutils installed
nslookup example.com
```

## Simple HTTP checks

- Fetch headers or content:
```bash
curl -I https://example.com    # headers only
curl -sS https://example.com    # content (silent on progress)
```

- Check response time and status:
```bash
curl -w "%{http_code} %{time_total}s\n" -o /dev/null -s https://example.com
```

## System resource monitoring

- View top CPU-consuming processes:
```bash
top
htop    # interactive, install with: sudo apt install htop
```

- One-shot process listing sorted by memory or CPU:
```bash
ps aux --sort=-%mem | head -n 15
ps aux --sort=-%cpu | head -n 15
```

- Show system uptime and load averages:
```bash
uptime
```

- Show free memory and swap:
```bash
free -h
```

- Real-time I/O/utilization (install sysstat for iostat):
```bash
vmstat 1 5
iostat -x 1 3   # needs sysstat package
```

## Disk and filesystem usage

- Show mounted filesystems and free space:
```bash
df -h
```

- Show directory sizes (human-readable):
```bash
du -sh /var/log/*
du -h --max-depth=1 /home/username
```

## Logs and system messages

- View kernel ring buffer (recent boot messages):
```bash
dmesg | less
```

- Query the systemd journal (requires journalctl):
```bash
sudo journalctl -b        # logs from current boot
sudo journalctl -u sshd   # logs for sshd service
sudo journalctl -f        # follow (like tail -f)
```

- Tail a log file in real time:
```bash
sudo tail -n 200 -f /var/log/syslog   # Debian/Ubuntu
sudo tail -n 200 -f /var/log/messages # CentOS/RHEL
```

## Network load and traffic

- Show per-connection bandwidth (install iftop):
```bash
sudo iftop -i eth0
```

- Monitor packet counts and errors:
```bash
ip -s link show dev eth0
```

## Quick checks and summaries

- Check DNS resolution chain and RTTs:
```bash
ping -c 3 google.com && dig +short google.com
```

- Summarize CPU, memory, and disk quickly:
```bash
echo "CPU: $(lscpu | grep '^Model name')"; free -h; df -h | head -n 5
```

## Notes

- Many network and monitoring tools require installation (e.g., traceroute, htop, iftop, iostat, dig). Use your distro package manager to install them.
- Use `sudo` for privileged operations. Be careful when following examples on production systems.

