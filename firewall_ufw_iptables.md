# Firewall (UFW/iptables) Cheatsheet

This cheatsheet covers common commands for managing firewalls on Linux using UFW (Uncomplicated Firewall) and iptables.

## UFW (Uncomplicated Firewall)

UFW is a user-friendly frontend for `iptables`, primarily used on Debian/Ubuntu-based systems. All commands typically require `sudo`.

*   **Check UFW Status**:
    ```bash
    sudo ufw status
    # For more detailed output:
    # sudo ufw status verbose
    # To see numbered rules (useful for deleting):
    # sudo ufw status numbered
    ```
*   **Enable UFW**:
    ```bash
    sudo ufw enable
    # Warning: Enabling UFW might block SSH if not explicitly allowed.
    # Ensure SSH is allowed before enabling on a remote server:
    # sudo ufw allow ssh
    # sudo ufw allow 22/tcp # If sshd runs on a non-standard port, use that port.
    ```
*   **Disable UFW**:
    ```bash
    sudo ufw disable
    ```
*   **Default Policies**: Define what to do with traffic that doesn't match any rule.
    *   Deny all incoming traffic by default (recommended):
        ```bash
        sudo ufw default deny incoming
        ```
    *   Allow all outgoing traffic by default (common):
        ```bash
        sudo ufw default allow outgoing
        ```
    *   Deny all outgoing traffic by default (more restrictive):
        ```bash
        sudo ufw default deny outgoing
        ```
*   **Allowing Connections**:
    *   By service name (uses `/etc/services`):
        ```bash
        sudo ufw allow ssh    # Allows TCP/UDP on port 22
        sudo ufw allow http   # Allows TCP on port 80
        sudo ufw allow https  # Allows TCP on port 443
        ```
    *   By port number:
        ```bash
        sudo ufw allow 22/tcp      # Allow TCP traffic on port 22
        sudo ufw allow 53/udp      # Allow UDP traffic on port 53
        sudo ufw allow 1000:2000/tcp # Allow TCP traffic on port range 1000-2000
        ```
    *   Allowing from a specific IP address:
        ```bash
        sudo ufw allow from 192.168.1.100
        ```
    *   Allowing from a specific IP address to a specific port and protocol:
        ```bash
        sudo ufw allow from 192.168.1.100 to any port 22 proto tcp
        ```
    *   Allowing from a specific subnet:
        ```bash
        sudo ufw allow from 192.168.0.0/24 to any port 3306 proto tcp # Example for MySQL
        ```
*   **Denying Connections**:
    *   Deny traffic on a port:
        ```bash
        sudo ufw deny 8080
        sudo ufw deny 1234/udp
        ```
    *   Deny traffic from a specific IP address:
        ```bash
        sudo ufw deny from 203.0.113.45
        ```
    *   Deny traffic from a specific IP to a specific port:
        ```bash
        sudo ufw deny from 203.0.113.45 to any port 80
        ```
*   **Deleting Rules**:
    *   By specifying the rule exactly as it was added:
        ```bash
        sudo ufw delete allow 80/tcp
        sudo ufw delete deny from 203.0.113.45
        ```
    *   By rule number (get numbers from `sudo ufw status numbered`):
        ```bash
        sudo ufw delete 1 # Deletes rule number 1
        ```
*   **Rate Limiting Connections** (helps prevent brute-force attacks):
    *   Limit SSH connections (denies if an IP makes 6+ connection attempts in 30 seconds):
        ```bash
        sudo ufw limit ssh
        # This is equivalent to:
        # sudo ufw limit 22/tcp
        ```
*   **Application Profiles**: Some applications install UFW profiles.
    *   List available application profiles:
        ```bash
        sudo ufw app list
        ```
    *   View information about a profile:
        ```bash
        sudo ufw app info 'Nginx Full'
        ```
    *   Allow traffic for an application profile:
        ```bash
        sudo ufw allow 'Nginx HTTP'
        ```
*   **Logging**:
    *   Enable logging:
        ```bash
        sudo ufw logging on # or low, medium, high, full
        ```
    *   Disable logging:
        ```bash
        sudo ufw logging off
        ```
    *   Logs are typically found in `/var/log/ufw.log`.
*   **Reset UFW** (disables UFW and deletes all rules):
    ```bash
    sudo ufw reset
    ```

## iptables

`iptables` is a powerful, low-level netfilter utility for configuring Linux kernel firewall rules. Commands require `sudo`. It's more complex than UFW.

*   **Core Concepts**:
    *   **Tables**: Contain chains and rules. Main tables:
        *   `filter`: Default table, for packet filtering.
        *   `nat`: For Network Address Translation (e.g., port forwarding, masquerading).
        *   `mangle`: For specialized packet alteration.
        *   `raw`: For configuring exemptions from connection tracking.
    *   **Chains**: Sequences of rules. Standard chains in `filter` table:
        *   `INPUT`: For packets destined for the local server.
        *   `OUTPUT`: For packets originating from the local server.
        *   `FORWARD`: For packets routed through the server.
    *   **Rules**: Conditions that packets are matched against and actions to take.
    *   **Targets (Actions)**: What to do if a packet matches a rule. Common targets:
        *   `ACCEPT`: Allow the packet.
        *   `DROP`: Silently discard the packet.
        *   `REJECT`: Discard the packet and send an error response (e.g., ICMP port unreachable).
        *   `LOG`: Log the packet (kernel logs, view with `dmesg` or in `/var/log/syslog`).
        *   `MASQUERADE` (in `nat` table, `POSTROUTING` chain): For NATing outgoing traffic.

*   **Listing Rules**:
    *   List rules in the `filter` table (default):
        ```bash
        sudo iptables -L -v -n --line-numbers
        # -L: List rules
        # -v: Verbose output (shows interface, packet/byte counts)
        # -n: Numeric output (don't resolve IPs/ports to names)
        # --line-numbers: Show rule numbers (useful for inserting/deleting)
        ```
    *   List rules for a specific chain:
        ```bash
        sudo iptables -L INPUT -v -n
        ```
    *   List rules for the `nat` table:
        ```bash
        sudo iptables -t nat -L -v -n
        ```
*   **Flushing Rules** (deleting all rules in a chain or all chains):
    *   Flush all rules in all chains (`filter` table):
        ```bash
        sudo iptables -F
        ```
    *   Flush rules in a specific chain:
        ```bash
        sudo iptables -F INPUT
        ```
    *   Flush rules in all chains for the `nat` table:
        ```bash
        sudo iptables -t nat -F
        ```
    *   Delete non-default chains (user-defined chains):
        ```bash
        sudo iptables -X
        ```
*   **Setting Default Policies (Chain Policies)**: This is the action taken if no rule in the chain matches a packet.
    *   Set default policy for INPUT chain to DROP:
        ```bash
        sudo iptables -P INPUT DROP
        ```
    *   Set default policy for FORWARD chain to DROP:
        ```bash
        sudo iptables -P FORWARD DROP
        ```
    *   Set default policy for OUTPUT chain to ACCEPT (common):
        ```bash
        sudo iptables -P OUTPUT ACCEPT
        ```
    **Important**: Set default policies to DROP *after* you have added rules to allow essential traffic (like SSH).

*   **Adding Rules (`-A` to append, `-I` to insert at a specific position)**:
    *   Allow established and related connections (essential for stateful firewall):
        ```bash
        sudo iptables -A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
        sudo iptables -A OUTPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT # If OUTPUT policy is DROP
        ```
    *   Allow loopback traffic (localhost communication):
        ```bash
        sudo iptables -A INPUT -i lo -j ACCEPT
        sudo iptables -A OUTPUT -o lo -j ACCEPT # If OUTPUT policy is DROP
        ```
    *   Allow SSH connections (TCP port 22):
        ```bash
        sudo iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
        ```
    *   Allow HTTP (TCP port 80) and HTTPS (TCP port 443):
        ```bash
        sudo iptables -A INPUT -p tcp --dport 80 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
        sudo iptables -A INPUT -p tcp --dport 443 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
        ```
    *   Allow traffic from a specific IP address:
        ```bash
        sudo iptables -A INPUT -s 192.168.1.100 -j ACCEPT
        ```
    *   Allow traffic from a specific IP to a specific port:
        ```bash
        sudo iptables -A INPUT -p tcp -s 192.168.1.100 --dport 3306 -j ACCEPT # Example for MySQL
        ```
    *   Allow traffic from a specific subnet:
        ```bash
        sudo iptables -A INPUT -p tcp -s 192.168.0.0/24 --dport 22 -j ACCEPT
        ```
    *   Drop packets from a specific IP (blacklisting):
        ```bash
        sudo iptables -A INPUT -s 203.0.113.50 -j DROP
        # Or insert at the top of the INPUT chain to ensure it's processed first
        # sudo iptables -I INPUT 1 -s 203.0.113.50 -j DROP
        ```
    *   Log dropped packets (before dropping them):
        ```bash
        sudo iptables -A INPUT -m limit --limit 5/min -j LOG --log-prefix "iptables_INPUT_denied: " --log-level 7
        # Then add a general drop rule if your policy isn't DROP already
        # sudo iptables -A INPUT -j DROP
        ```
*   **Deleting Rules**:
    *   By specifying the rule exactly:
        ```bash
        sudo iptables -D INPUT -p tcp --dport 80 -j ACCEPT
        ```
    *   By chain and rule number (get numbers from `sudo iptables -L --line-numbers`):
        ```bash
        sudo iptables -D INPUT 3 # Deletes rule number 3 in the INPUT chain
        ```
*   **Replacing Rules (`-R`)**:
    ```bash
    sudo iptables -R INPUT 1 -s 192.168.1.200 -j DROP # Replace rule 1 in INPUT chain
    ```
*   **NAT (Network Address Translation) Example - Masquerading**:
    Allows hosts on a private network (e.g., 192.168.0.0/24 on eth1) to access the internet through the Linux server's public interface (e.g., eth0).
    1.  Enable IP forwarding:
        ```bash
        echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
        # Make permanent by editing /etc/sysctl.conf: net.ipv4.ip_forward=1
        # Then run: sudo sysctl -p
        ```
    2.  Add MASQUERADE rule to `nat` table, `POSTROUTING` chain:
        ```bash
        sudo iptables -t nat -A POSTROUTING -o eth0 -s 192.168.0.0/24 -j MASQUERADE
        ```
    3.  Ensure FORWARD chain allows this traffic:
        ```bash
        sudo iptables -A FORWARD -i eth1 -o eth0 -s 192.168.0.0/24 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
        sudo iptables -A FORWARD -i eth0 -o eth1 -d 192.168.0.0/24 -j ACCEPT # Allow replies back
        # Or, if your FORWARD policy is ACCEPT and you trust the internal network:
        # sudo iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
        ```
*   **NAT Example - Port Forwarding (DNAT)**:
    Forward traffic arriving on the server's public IP (e.g., on eth0, port 8080) to an internal server (e.g., 192.168.1.50 on port 80).
    1.  Enable IP forwarding (as above).
    2.  Add DNAT rule to `nat` table, `PREROUTING` chain:
        ```bash
        sudo iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 8080 -j DNAT --to-destination 192.168.1.50:80
        ```
    3.  Ensure FORWARD chain allows this traffic:
        ```bash
        sudo iptables -A FORWARD -i eth0 -o <internal_interface> -p tcp --dport 80 -d 192.168.1.50 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
        ```

*   **Saving and Restoring iptables Rules**: Rules are lost on reboot by default.
    *   **Debian/Ubuntu**: Use `iptables-persistent` package.
        ```bash
        sudo apt-get install iptables-persistent
        # During installation, it will ask to save current IPv4 and IPv6 rules.
        # To save rules manually later:
        # sudo netfilter-persistent save
        # sudo netfilter-persistent reload
        # Rules are typically saved to /etc/iptables/rules.v4 and /etc/iptables/rules.v6
        ```
    *   **RHEL/CentOS (older versions using iptables service)**:
        ```bash
        sudo yum install iptables-services
        sudo systemctl enable iptables
        sudo systemctl start iptables
        sudo iptables-save > /etc/sysconfig/iptables
        sudo ip6tables-save > /etc/sysconfig/ip6tables
        # Then restart service: sudo systemctl restart iptables
        ```
    *   **Generic manual save/restore**:
        ```bash
        # Save rules
        sudo iptables-save > /etc/iptables.rules
        # Restore rules (e.g., in a startup script)
        sudo iptables-restore < /etc/iptables.rules
        ```

This detailed update for `firewall_ufw_iptables.md` covers common use cases for both UFW and iptables. Next, I'll enhance `nmap.md`.The `firewall_ufw_iptables.md` cheatsheet has been successfully updated with detailed command examples for both UFW and iptables, covering common scenarios, rule management, and persistence.

Next, I will enhance `nmap.md` by providing more specific command examples for various scan types, target specifications, and output formatting.
