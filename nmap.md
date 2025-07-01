# nmap Cheatsheet

*   **Purpose**: Network discovery and security auditing.
*   **Common Scan Types**:
    *   Ping Scan (Host Discovery): `nmap -sn target_network` (e.g., `192.168.1.0/24`). No port scan.
    *   TCP SYN Scan (Default, Stealthy): `nmap -sS target_host`.
    *   TCP Connect Scan: `nmap -sT target_host` (full TCP handshake, more detectable).
    *   UDP Scan: `nmap -sU target_host` (slower, often combined with `-p` for specific ports).
    *   Version Detection: `nmap -sV target_host` (tries to determine service/version on open ports).
    *   OS Detection: `nmap -O target_host` (requires root/admin).
    *   Aggressive Scan: `nmap -A target_host` (enables OS detection, version detection, script scanning, and traceroute).
    *   Script Scanning (NSE - Nmap Scripting Engine): `nmap -sC target_host` (default scripts) or `nmap --script <script-name_or_category> target_host`.
*   **Target Specification**: Single IP, hostname, network range (e.g., `192.168.1.1-100`, `192.168.1.0/24`), list from file (`-iL file.txt`).
*   **Port Specification**:
    *   Default: Scans 1000 most common TCP ports.
    *   Specific ports: `-p 80,443,8080`.
    *   Port range: `-p 1-1024`.
    *   All ports: `-p-` (or `-p 1-65535`).
    *   Fast scan (fewer ports): `-F`.
*   **Timing and Performance**:
    *   Timing templates: `-T0` (paranoid) to `-T5` (insane). Default is `-T3`. `-T4` is common for faster scans.
*   **Output Formats**:
    *   Normal: Default console output.
    *   XML: `-oX output.xml`.
    *   Grepable: `-oG output.grep`.
    *   Script Kiddie: `-oS output.skriptkiddie`.
    *   All formats: `-oA basename`.
*   **Examples**:
    *   Scan top ports on a host: `nmap target.example.com`
    *   Discover live hosts on a network: `nmap -sn 192.168.1.0/24`
    *   Scan specific TCP ports with version detection: `nmap -sV -p 22,80,443 target.example.com`
    *   Run default vulnerability scripts: `nmap --script vuln target.example.com`
*   **Ethical Use**: Only scan networks/hosts you have explicit permission to scan.
