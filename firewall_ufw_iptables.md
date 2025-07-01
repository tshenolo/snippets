# Firewall (UFW/iptables) Cheatsheet

*   **UFW (Uncomplicated Firewall) - Frontend for iptables**:
    *   Purpose: Simplify firewall management on Linux.
    *   Status: `sudo ufw status` or `sudo ufw status verbose`.
    *   Enable/Disable: `sudo ufw enable`, `sudo ufw disable`.
    *   Default Policies:
        *   `sudo ufw default deny incoming`
        *   `sudo ufw default allow outgoing`
    *   Allowing Connections:
        *   By port: `sudo ufw allow 22` (for SSH) or `sudo ufw allow 22/tcp`.
        *   By service name: `sudo ufw allow ssh` (uses `/etc/services`).
        *   Specific IP: `sudo ufw allow from 192.168.1.100`.
        *   Specific IP and port: `sudo ufw allow from 192.168.1.100 to any port 22 proto tcp`.
    *   Denying Connections: `sudo ufw deny 80`.
    *   Deleting Rules: `sudo ufw delete allow 80` or by number `sudo ufw status numbered`, then `sudo ufw delete <number>`.
    *   Rate Limiting: `sudo ufw limit ssh`.
*   **iptables - Low-level packet filtering**:
    *   Concepts: Tables (filter, nat, mangle, raw), Chains (INPUT, OUTPUT, FORWARD, PREROUTING, POSTROUTING), Rules, Targets (ACCEPT, DROP, REJECT, LOG).
    *   Listing Rules: `sudo iptables -L -v -n` (for filter table). `sudo iptables -t nat -L -v -n` (for NAT table).
    *   Flushing Rules: `sudo iptables -F` (flush all rules in filter table).
    *   Setting Default Policies:
        *   `sudo iptables -P INPUT DROP`
        *   `sudo iptables -P FORWARD DROP`
        *   `sudo iptables -P OUTPUT ACCEPT`
    *   Allowing Specific Traffic (Examples):
        *   Allow established connections: `sudo iptables -A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT`
        *   Allow loopback: `sudo iptables -A INPUT -i lo -j ACCEPT`
        *   Allow SSH: `sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT`
        *   Allow HTTP/HTTPS: `sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT`, `sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT`
    *   Saving Rules: Varies by distro (e.g., `iptables-save > /etc/iptables/rules.v4` and `iptables-persistent` package on Debian/Ubuntu).
    *   Logging Dropped Packets: `sudo iptables -A INPUT -m limit --limit 5/min -j LOG --log-prefix "iptables_INPUT_denied: " --log-level 7` (then drop).
