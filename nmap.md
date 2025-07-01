# nmap (Network Mapper) Cheatsheet

Nmap is a powerful open-source tool for network discovery, security auditing, and port scanning.
**Ethical Use**: Only scan networks and hosts you have explicit permission to scan. Unauthorized scanning can be illegal.

## Basic Syntax

```bash
nmap [Scan Type(s)] [Options] {target specification}
```

## Target Specification

*   **Single IP Address**:
    ```bash
    nmap 192.168.1.1
    ```
*   **Hostname**:
    ```bash
    nmap server.example.com
    ```
*   **Multiple IP Addresses**:
    ```bash
    nmap 192.168.1.1 192.168.1.2 10.0.0.5
    ```
*   **CIDR Notation (Network Range)**:
    ```bash
    nmap 192.168.1.0/24 # Scans 192.168.1.0 to 192.168.1.255
    ```
*   **Octet Range Addressing**:
    ```bash
    nmap 192.168.1.1-100 # Scans 192.168.1.1 through 192.168.1.100
    nmap 192.168.1,2,3.5,6 # Scans 192.168.1.5, 192.168.1.6, 192.168.2.5, ..., 192.168.3.6
    ```
*   **Input from a File (`-iL`)**:
    ```bash
    nmap -iL targets.txt # targets.txt contains a list of hosts/networks, one per line
    ```
*   **Exclude Hosts (`--exclude`)**:
    ```bash
    nmap 192.168.1.0/24 --exclude 192.168.1.5,192.168.1.10
    ```
*   **Exclude Hosts from a File (`--excludefile`)**:
    ```bash
    nmap 192.168.1.0/24 --excludefile excluded_hosts.txt
    ```
*   **Random Targets (`-iR`)**:
    ```bash
    nmap -iR 10 # Choose 10 random hosts from the internet to scan (use with extreme caution and legal permission)
    ```

## Scan Types

*   **Ping Scan / Host Discovery (`-sn` or `-sP`)**: Discovers live hosts without port scanning.
    ```bash
    nmap -sn 192.168.1.0/24
    # -sP is an older alias for -sn
    ```
    *   Disable ping (`-Pn` or `-P0`): Skips host discovery and scans every target IP as if it's online. Useful if hosts block pings.
        ```bash
        nmap -Pn 192.168.1.10 # Warning: Can be very slow if hosts are down
        ```
*   **TCP SYN Scan (`-sS`)**: Default scan type if run as root/administrator. Stealthy, as it doesn't complete TCP connections.
    ```bash
    sudo nmap -sS target.example.com
    ```
*   **TCP Connect Scan (`-sT`)**: Default if SYN scan is not available (e.g., non-root user). Completes TCP handshake, more detectable.
    ```bash
    nmap -sT target.example.com
    ```
*   **UDP Scan (`-sU`)**: Scans UDP ports. Often slower and more difficult due to UDP's connectionless nature.
    ```bash
    sudo nmap -sU target.example.com
    # Often combined with -p for specific UDP ports or --top-ports
    # sudo nmap -sU -p 53,161,162 target.example.com
    ```
*   **TCP ACK Scan (`-sA`)**: Used to map out firewall rulesets, determining if they are stateful or just simple packet filters.
    ```bash
    sudo nmap -sA target.example.com
    ```
*   **TCP Window Scan (`-sW`)**: Similar to ACK scan but can sometimes differentiate open ports from closed ones on certain systems.
    ```bash
    sudo nmap -sW target.example.com
    ```
*   **TCP FIN, Xmas, Null Scans (`-sF`, `-sX`, `-sN`)**: Stealthy scans that can bypass some non-stateful firewalls. Less reliable than SYN scan.
    ```bash
    sudo nmap -sF target.example.com # FIN scan
    sudo nmap -sX target.example.com # Xmas scan
    sudo nmap -sN target.example.com # Null scan
    ```
*   **SCTP INIT Scan (`-sY`)**: Scans for SCTP (Stream Control Transmission Protocol) ports.
    ```bash
    sudo nmap -sY target.example.com
    ```
*   **IP Protocol Scan (`-sO`)**: Determines which IP protocols (TCP, UDP, ICMP, etc.) are supported by target hosts.
    ```bash
    sudo nmap -sO target.example.com
    ```

## Port Specification and Scan Order

*   **Scan Specific Ports (`-p`)**:
    ```bash
    nmap -p 80 target.example.com # Scan only port 80
    nmap -p 22,80,443 target.example.com # Scan ports 22, 80, and 443
    nmap -p 1-1024 target.example.com # Scan ports from 1 to 1024
    nmap -p U:53,111,137,T:21-25,80,139,8080 target.example.com # Mix UDP and TCP ports
    nmap -p- target.example.com # Scan all 65535 ports (TCP by default)
    ```
*   **Scan Top N Ports (`--top-ports`)**: Scans the N most common ports.
    ```bash
    nmap --top-ports 10 target.example.com # Scan the 10 most common ports
    ```
*   **Fast Scan Mode (`-F`)**: Scans fewer ports than the default scan (top 100 ports).
    ```bash
    nmap -F target.example.com
    ```
*   **Don't Randomize Port Scan Order (`-r`)**: Scans ports sequentially. Default is randomized.
    ```bash
    nmap -r target.example.com
    ```

## Service and Version Detection

*   **Version Detection (`-sV` or `-A`)**: Tries to determine the service/version running on open ports.
    ```bash
    sudo nmap -sV target.example.com
    # -A enables OS detection, version detection, script scanning, and traceroute
    # sudo nmap -A target.example.com
    ```
*   **Version Intensity (`--version-intensity <0-9>`)**: Set from 0 (light) to 9 (try all probes). Default is 7.
    ```bash
    sudo nmap -sV --version-intensity 5 target.example.com
    ```
*   **Version Light (`--version-light`)**: Alias for `--version-intensity 2`.
*   **Version All (`--version-all`)**: Alias for `--version-intensity 9`.

## OS Detection (`-O`)

*   **Enable OS Detection (`-O` or `-A`)**: Tries to determine the operating system of the target. Requires root/administrator privileges.
    ```bash
    sudo nmap -O target.example.com
    # sudo nmap -A target.example.com (also enables -O)
    ```
*   **Limit OS Detection (`--osscan-limit`)**: If no open and closed TCP ports are found, OS detection is skipped. This option makes Nmap try OS detection anyway.
    ```bash
    sudo nmap -O --osscan-limit target.example.com
    ```
*   **Guess OS More Aggressively (`--osscan-guess` or `--fuzzy`)**:
    ```bash
    sudo nmap -O --osscan-guess target.example.com
    ```

## Nmap Scripting Engine (NSE)

NSE allows users to write (and share) scripts to automate a wide variety of networking tasks. Scripts are written in Lua.

*   **Run Default Scripts (`-sC` or `-A`)**: Equivalent to `--script=default`.
    ```bash
    nmap -sC target.example.com
    # nmap -A target.example.com (also enables -sC)
    ```
*   **Run Specific Script(s) (`--script`)**:
    ```bash
    nmap --script=http-title target.example.com # Run a single script
    nmap --script=http-*,smb-os-discovery target.example.com # Run scripts matching patterns
    nmap --script=/path/to/custom_script.nse target.example.com # Run a custom script
    ```
*   **Run Scripts from Categories**:
    ```bash
    nmap --script=vuln target.example.com # Run all scripts in the 'vuln' category
    # Common categories: auth, broadcast, default, discovery, dos, exploit, external, fuzzer, intrusive, malware, safe, version, vuln
    ```
*   **Update Script Database (`--script-updatedb`)**: Updates the script database.
    ```bash
    sudo nmap --script-updatedb
    ```
*   **Get Help on a Script (`--script-help`)**:
    ```bash
    nmap --script-help http-title
    ```
*   **Pass Arguments to Scripts (`--script-args`)**:
    ```bash
    nmap --script http-enum --script-args http.maxfiles=10 target.example.com
    nmap -p80 --script http-default-accounts --script-args http-default-accounts.fingerprintfile=nselib/data/http-fingerprints.lua target.example.com
    ```

## Timing and Performance

*   **Timing Templates (`-T<0-5>`)**: Adjusts scan speed and aggressiveness.
    *   `-T0` (paranoid): Very slow, for IDS evasion.
    *   `-T1` (sneaky): Quite slow.
    *   `-T2` (polite): Slows down to consume less bandwidth/resources.
    *   `-T3` (normal): Default.
    *   `-T4` (aggressive): Assumes a fast and reliable network. Speeds up scans.
    *   `-T5` (insane): Very aggressive, may sacrifice accuracy for speed.
    ```bash
    nmap -T4 target.example.com
    ```
*   **Set Minimum Host Group Size (`--min-hostgroup`) / Maximum Host Group Size (`--max-hostgroup`)**: Affects parallel scanning.
*   **Set Minimum Parallelism (`--min-parallelism`) / Maximum Parallelism (`--max-parallelism`)**: Controls number of probes outstanding.
*   **Set Minimum RTT Timeout (`--min-rtt-timeout`) / Maximum RTT Timeout (`--max-rtt-timeout`) / Initial RTT Timeout (`--initial-rtt-timeout`)**.
*   **Set Maximum Retries (`--max-retries`)**.
*   **Set Scan Delay (`--scan-delay <time>`)**: Wait at least `<time>` between probes (e.g., `1s`, `500ms`).
*   **Set Host Timeout (`--host-timeout <time>`)**: Give up on target after this long.

## Firewall/IDS Evasion and Spoofing (Use with extreme caution and knowledge)

*   **Fragment Packets (`-f`)**: Splits packets into smaller fragments.
    ```bash
    sudo nmap -f target.example.com
    # Can specify MTU with --mtu <value>
    ```
*   **Decoys (`-D`)**: Makes the scan appear to come from other (decoy) IPs as well as your own.
    ```bash
    sudo nmap -D RND:10 target.example.com # 10 random decoys + your IP
    sudo nmap -D decoy1,decoy2,ME,decoy3 target.example.com # ME is your actual IP
    ```
*   **Idle (Zombie) Scan (`-sI <zombie_host[:probeport]>`)**: A very stealthy scan that uses a "zombie" host to relay scan probes. Complex to set up and use.
*   **Source Port Spoofing (`--source-port <portnum>` or `-g <portnum>`)**: Use a specific source port.
*   **Spoof MAC Address (`--spoof-mac <MAC_address, prefix, or vendor_name>`)**:
    ```bash
    sudo nmap --spoof-mac 00:01:02:03:04:05 target.example.com
    sudo nmap --spoof-mac Apple target.example.com
    ```
*   **Send Bad Checksums (`--badsum`)**: Sends packets with incorrect TCP/UDP/SCTP checksums.

## Output Formats

*   **Normal Output (`-oN <filespec>`)**: Standard Nmap output.
    ```bash
    nmap -oN output.txt target.example.com
    ```
*   **XML Output (`-oX <filespec>`)**: Machine-readable XML format.
    ```bash
    nmap -oX output.xml target.example.com
    ```
*   **Script Kiddie Output (`-oS <filespec>`)**: L33t speak output (mostly for fun).
    ```bash
    nmap -oS output.skript target.example.com
    ```
*   **Grepable Output (`-oG <filespec>`)**: Easy to parse with tools like grep, awk.
    ```bash
    nmap -oG output.grep target.example.com
    ```
*   **All Formats (`-oA <basename>`)**: Saves in Normal, XML, and Grepable formats using `<basename>.nmap`, `<basename>.xml`, `<basename>.gnmap`.
    ```bash
    nmap -oA scan_results target.example.com
    ```
*   **Verbosity (`-v`, `-vv`)**: Increase verbosity of output.
    ```bash
    nmap -v target.example.com
    ```
*   **Debug Level (`-d`, `-dd`)**: Increase debugging level.
    ```bash
    nmap -d target.example.com
    ```
*   **Reason for Port State (`--reason`)**: Shows why Nmap concluded a port is open, closed, or filtered.
*   **Only Show Open Ports (`--open`)**:
    ```bash
    nmap --open target.example.com
    ```
*   **Packet Tracing (`--packet-trace`)**: Shows all packets sent and received.
*   **Resume Scan (`--resume <filename>`)**: Resume an aborted scan from Normal or Grepable output files.
    ```bash
    nmap --resume output.nmap # or output.gnmap
    ```

## Miscellaneous Options

*   **IPv6 Scanning (`-6`)**:
    ```bash
    nmap -6 ipv6.target.example.com
    ```
*   **Traceroute (`--traceroute`)**: Traces path to host (usually run after scan).
    ```bash
    nmap --traceroute target.example.com
    ```
*   **DNS Resolution**:
    *   `-n`: Never do DNS resolution.
    *   `-R`: Always do reverse DNS resolution (even for offline hosts).
    *   `--dns-servers <server1[,server2],...>`: Specify custom DNS servers.
*   **Privileged Operations**: Many scan types (SYN, OS detection, etc.) require root/administrator privileges. Nmap will usually tell you if you need them.
*   **Interface (`-e <interface>`)**: Specify which network interface to use.
    ```bash
    sudo nmap -e eth0 target.example.com
    ```

This detailed `nmap.md` should serve as a good reference. I'll move on to `fail2ban.md`.The `nmap.md` cheatsheet is now significantly more detailed, with extensive examples for various scan types, target specifications, NSE usage, and output options.

Next, I will enhance `fail2ban.md`. This will involve adding more specific examples for `fail2ban-client` commands and illustrating common jail configurations.
