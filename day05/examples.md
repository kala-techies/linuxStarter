
# Day 05 : Networking and System Monitoring (Examples)

The examples below provide step-by-step explanations and real-world use cases for common networking and monitoring commands.

## 1) Check network interfaces and IP addresses

Command:
```bash
ip addr show
```

Explanation:
- `ip addr show` lists all network interfaces and their addresses. Look for `inet` entries to find IPv4 addresses (e.g., `inet 192.168.1.10/24`).
- Use this to verify whether an interface has an IP, check link state (UP/DOWN), and view MAC addresses.

## 2) Test connectivity to a remote host

Command:
```bash
ping -c 4 8.8.8.8
```

Explanation:
- Sends 4 ICMP echo requests to Google's public DNS server. Useful to verify basic network connectivity and measure round-trip time (RTT).
- If pings fail, check `ip addr`, routing (`ip route`), and firewall rules.

## 3) Find which services are listening on ports

Command:
```bash
ss -tuln
```

Explanation:
- `ss` shows TCP/UDP sockets. `-tuln` filters for TCP/UDP listening sockets and displays numeric ports.
- Use this to check if a service (e.g., port 22 for SSH) is listening or to detect unexpected open ports.

## 4) Simple HTTP check with curl

Command:
```bash
curl -I https://example.com
```

Explanation:
- `-I` requests HTTP headers only. Useful to quickly check status code (200, 301, 404) and server headers.
- For more detailed timing, add `-w` to print elapsed time.

## 5) Trace network path to a remote host

Command:
```bash
traceroute example.com
```

Explanation:
- Shows each hop between your machine and the destination. Helps identify where latency or packet loss occurs on the route.
- If `traceroute` isn't installed, use `mtr` for combined traceroute/ping analysis.

## 6) Monitor CPU and memory usage

Command:
```bash
top
```

Explanation:
- `top` displays a live view of processes sorted by CPU by default. Look at the %CPU and %MEM columns to identify resource hogs.
- Use `htop` for a colored, interactive view (install if not present).

## 7) Find top memory consumers non-interactively

Command:
```bash
ps aux --sort=-%mem | head -n 15
```

Explanation:
- Shows the 15 processes using the most memory. Useful when you need a snapshot (for scripts or reports) rather than an interactive monitor.

## 8) Check disk usage for a filesystem

Command:
```bash
df -h /
```

Explanation:
- `df -h /` shows used and available space for the root filesystem in human-readable units. Check frequently on servers with limited disk space.

## 9) Find large directories under /var/log

Command:
```bash
du -sh /var/log/* | sort -hr | head -n 10
```

Explanation:
- `du -sh` prints sizes; piping to `sort -hr` orders from largest to smallest. Use this to locate log files or folders consuming space.

## 10) Inspect recent kernel messages

Command:
```bash
dmesg | tail -n 50
```

Explanation:
- `dmesg` prints kernel messages (driver initialization, hardware events). Tail the last entries to see recent kernel-level errors (e.g., disk, USB).

## 11) View system logs for a service

Command:
```bash
sudo journalctl -u sshd.service -n 200 --no-pager
```

Explanation:
- Shows the last 200 log lines for the `sshd` service from the systemd journal. Helpful for troubleshooting login or service start failures.

## 12) Follow a log file in real time

Command:
```bash
sudo tail -n 200 -f /var/log/syslog
```

Explanation:
- Use `-f` to follow new log lines appended to the file. This is invaluable during deployments or when reproducing an issue.

## 13) Quick DNS lookup

Command:
```bash
dig +short example.com
```

Explanation:
- `dig +short` returns the resolved IPs for a hostname. Good for automating checks or quickly verifying DNS A records.

## 14) Combined quick health summary (one-liner)

Command:
```bash
echo "Uptime:"; uptime; echo "Memory:"; free -h; echo "Top disk usage:"; df -h / | tail -n 1
```

Explanation:
- A handy one-liner to gather basic health metrics (uptime, memory usage, root disk usage) for quick screening.

---

