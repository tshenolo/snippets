# fail2ban Cheatsheet

*   **Purpose**: Intrusion prevention software that monitors log files for malicious patterns and bans offending IPs using firewall rules.
*   **Configuration**:
    *   Main config: `/etc/fail2ban/fail2ban.conf` (usually not modified directly).
    *   Local overrides: `/etc/fail2ban/fail2ban.local`.
    *   Jail config: `/etc/fail2ban/jail.conf` (contains default jails, not modified directly).
    *   Local jail overrides: `/etc/fail2ban/jail.local` (primary file for customization) or individual files in `/etc/fail2ban/jail.d/`.
*   **Jail Setup (`jail.local`)**:
    *   `[DEFAULT]` section: Global settings (e.g., `bantime`, `findtime`, `maxretry`).
    *   Specific Jails: `[sshd]`, `[apache-auth]`, etc.
        *   `enabled = true/false`: Activates or deactivates the jail.
        *   `port = ssh` (or port number).
        *   `filter = sshd` (name of the filter file in `/etc/fail2ban/filter.d/`).
        *   `logpath = /var/log/auth.log` (path to the log file to monitor).
        *   `maxretry = 5`: Number of failures before banning.
        *   `bantime = 1h` (1 hour), `1d` (1 day), `-1` (permanent).
        *   `findtime = 10m`: Time window in which `maxretry` must occur.
        *   `action = %(action_)s` (default action), `%(action_mw)s` (ban & mail), `%(action_mwl)s` (ban & mail with whois and logs).
*   **Filter Files (`/etc/fail2ban/filter.d/*.conf`)**: Contain regular expressions (`failregex`) to detect malicious attempts.
*   **Actions (`/etc/fail2ban/action.d/*.conf`)**: Define commands to execute when an IP is banned/unbanned (e.g., adding/removing iptables rules).
*   **Client (`fail2ban-client`)**:
    *   Status: `sudo fail2ban-client status`.
    *   Status of a specific jail: `sudo fail2ban-client status sshd`.
    *   Unban IP: `sudo fail2ban-client set sshd unbanip 1.2.3.4`.
    *   Reload configuration: `sudo fail2ban-client reload`.
*   **Example Jail for SSH**:
    ```ini
    # In /etc/fail2ban/jail.local
    [sshd]
    enabled = true
    port = ssh
    filter = sshd
    logpath = /var/log/auth.log # For Debian/Ubuntu; /var/log/secure for CentOS/RHEL
    maxretry = 3
    bantime = 1d
    ```
*   **Testing Filters**: `fail2ban-regex /var/log/auth.log /etc/fail2ban/filter.d/sshd.conf`.
