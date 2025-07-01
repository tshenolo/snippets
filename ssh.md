# SSH (Secure Shell) Cheatsheet

SSH is a cryptographic network protocol for operating network services securely over an unsecured network. Its most notable applications are remote login and command-line execution.

## Basic Connection

*   **Connect to a remote host**:
    ```bash
    ssh <username>@<hostname_or_ip>
    # Example:
    # ssh jdoe@server.example.com
    ```
*   **Connect on a specific port** (default is 22):
    ```bash
    ssh <username>@<hostname_or_ip> -p <port_number>
    # Example:
    # ssh jdoe@server.example.com -p 2222
    ```
*   **Connect with a specific identity file (private key)**:
    ```bash
    ssh -i /path/to/private_key <username>@<hostname_or_ip>
    # Example:
    # ssh -i ~/.ssh/id_rsa_personal jdoe@server.example.com
    ```
*   **Verbose output** (for debugging connection issues):
    ```bash
    ssh -v <username>@<hostname_or_ip> # More verbose: -vv, -vvv
    ```
*   **Execute a single command on the remote host**:
    ```bash
    ssh <username>@<hostname_or_ip> "ls -l /var/www"
    # Example:
    # ssh webadmin@server.example.com "sudo systemctl restart nginx"
    ```
    *Note: For commands requiring a TTY (like `sudo` without `NOPASSWD`), you might need `-t`.*
    ```bash
    ssh -t <username>@<hostname_or_ip> "sudo some_command"
    ```

## Public Key Authentication

More secure than password authentication. Consists of a private key (kept secret on your client) and a public key (placed on the server).

*   **Generate an SSH key pair** (on your client machine):
    *   RSA (common):
        ```bash
        ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
        # -b 4096 specifies a 4096-bit key (strong)
        # -C is an optional comment, often your email
        ```
    *   Ed25519 (more modern, faster, and secure):
        ```bash
        ssh-keygen -t ed25519 -C "your_email@example.com"
        ```
    *   This will typically create `~/.ssh/id_rsa` (private key) and `~/.ssh/id_rsa.pub` (public key), or `id_ed25519` and `id_ed25519.pub`. Protect your private key! You can add a passphrase for extra security.
*   **Copy your public key to the remote server** (easiest method):
    ```bash
    ssh-copy-id <username>@<hostname_or_ip>
    # If using a specific identity file:
    # ssh-copy-id -i ~/.ssh/id_rsa_personal.pub <username>@<hostname_or_ip>
    # If server uses a non-standard port:
    # ssh-copy-id -p <port_number> <username>@<hostname_or_ip>
    ```
*   **Manually copy public key** (if `ssh-copy-id` is not available):
    1.  Copy the content of your local `~/.ssh/id_rsa.pub` (or `id_ed25519.pub`).
    2.  SSH into the remote server using password authentication.
    3.  Append the copied public key content to `~/.ssh/authorized_keys` on the server:
        ```bash
        mkdir -p ~/.ssh
        chmod 700 ~/.ssh
        echo "PASTE_PUBLIC_KEY_CONTENT_HERE" >> ~/.ssh/authorized_keys
        chmod 600 ~/.ssh/authorized_keys
        ```
        Ensure `~/.ssh` directory has `700` permissions and `authorized_keys` file has `600` permissions.

## SSH Configuration File (`~/.ssh/config` on client)

Simplifies connecting to frequently used hosts.

*   **Example `~/.ssh/config` entry**:
    ```
    Host myserver
        HostName server.example.com
        User jdoe
        Port 2222
        IdentityFile ~/.ssh/id_rsa_personal
        ForwardAgent yes # Be cautious with ForwardAgent

    Host another-server
        HostName 192.168.1.100
        User admin
        # Uses default port 22 and default identity files like ~/.ssh/id_rsa
    ```
*   **With this config, you can connect using**:
    ```bash
    ssh myserver
    ssh another-server
    ```
*   **Common `~/.ssh/config` options**:
    *   `Host`: Alias for the connection.
    *   `HostName`: Actual hostname or IP address.
    *   `User`: Default username for this host.
    *   `Port`: SSH port on the remote host.
    *   `IdentityFile`: Path to the private key to use.
    *   `IdentitiesOnly yes`: Only use specified IdentityFile(s), don't try default keys.
    *   `ForwardAgent yes|no`: Enables/disables SSH agent forwarding (see security implications).
    *   `RequestTTY yes|force|no|auto`: Controls TTY allocation.
    *   `LocalForward`: Local port forwarding configuration.
    *   `RemoteForward`: Remote port forwarding configuration.
    *   `DynamicForward`: SOCKS proxy configuration.
    *   `ProxyCommand` or `ProxyJump`: For connecting through a bastion/jump host.
        ```
        Host target-server
            HostName internal.example.com
            User myuser
            ProxyJump bastion.example.com # Connect via bastion.example.com (user defaults to current or from bastion's config)
            # Or, for older SSH versions or more control:
            # ProxyCommand ssh bastion.example.com -W %h:%p
        ```
    *   `ServerAliveInterval <seconds>`: Sends a keep-alive message every N seconds.
    *   `ServerAliveCountMax <count>`: Disconnects if N keep-alive messages fail.

## SSH Agent

Manages your private keys and their passphrases, so you don't have to type them repeatedly.

*   **Start the SSH agent** (often started automatically with your desktop session):
    ```bash
    eval "$(ssh-agent -s)"
    ```
*   **Add a private key to the agent**:
    ```bash
    ssh-add /path/to/your/private_key
    # Example:
    # ssh-add ~/.ssh/id_rsa
    # (Will prompt for passphrase if the key has one)
    ```
*   **List keys currently managed by the agent**:
    ```bash
    ssh-add -l
    ```
*   **Remove a specific key from the agent**:
    ```bash
    ssh-add -d /path/to/your/private_key
    ```
*   **Remove all keys from the agent**:
    ```bash
    ssh-add -D
    ```
*   **Agent Forwarding (`-A` option or `ForwardAgent yes` in config)**: Allows you to use your local SSH keys to authenticate from a remote server to another server.
    ```bash
    ssh -A user@jumphost
    # Now, from jumphost:
    # ssh user@internal_server # Uses keys from your local agent
    ```
    **Security Warning**: Use agent forwarding with caution. If the jump host is compromised, an attacker could potentially use your forwarded agent connection.

## File Transfer with `scp` and `sftp`

*   **`scp` (Secure Copy)**:
    *   Copy a file from local to remote:
        ```bash
        scp /path/to/local/file.txt <username>@<hostname>:/path/to/remote/directory/
        # Example:
        # scp report.pdf jdoe@server.example.com:/home/jdoe/documents/
        ```
    *   Copy a file from remote to local:
        ```bash
        scp <username>@<hostname>:/path/to/remote/file.txt /path/to/local/directory/
        # Example:
        # scp jdoe@server.example.com:/var/log/app.log ./logs/
        ```
    *   Copy a directory recursively (`-r`):
        ```bash
        scp -r /path/to/local/directory <username>@<hostname>:/path/to/remote/parent_directory/
        scp -r <username>@<hostname>:/path/to/remote/directory /path/to/local/parent_directory/
        ```
    *   Specify port (`-P`, uppercase P for scp):
        ```bash
        scp -P <port_number> file.txt <username>@<hostname>:/remote/path/
        ```
    *   Use a specific identity file (`-i`):
        ```bash
        scp -i ~/.ssh/id_rsa_other key.pem <username>@<hostname>:/remote/path/
        ```
*   **`sftp` (SSH File Transfer Protocol)**: Interactive file transfer session.
    *   Connect to an SFTP server:
        ```bash
        sftp <username>@<hostname_or_ip>
        # sftp -P <port_number> <username>@<hostname>
        # sftp -i /path/to/private_key <username>@<hostname>
        ```
    *   **Common SFTP commands** (inside the `sftp>` prompt):
        *   `help`: Show available commands.
        *   `ls`, `lls`: List remote/local files.
        *   `cd <path>`, `lcd <path>`: Change remote/local directory.
        *   `pwd`, `lpwd`: Print remote/local working directory.
        *   `get <remote_file> [local_file]`: Download file.
        *   `put <local_file> [remote_file]`: Upload file.
        *   `mget <remote_pattern>`: Download multiple files.
        *   `mput <local_pattern>`: Upload multiple files.
        *   `mkdir <dir>`, `lmkdir <dir>`: Create remote/local directory.
        *   `rm <file>`, `rmdir <dir>`: Remove remote file/directory.
        *   `rename <old> <new>`: Rename remote file.
        *   `bye` or `quit` or `exit`: Close SFTP session.

## SSH Tunneling (Port Forwarding)

*   **Local Port Forwarding (`-L`)**: Access a service on a remote network as if it were local.
    `ssh -L <local_port_to_listen_on>:<remote_destination_host>:<remote_destination_port> <username>@<ssh_server_host>`
    *   Example: Access a database (PostgreSQL on port 5432) running on `db.internal.example.com` (reachable from `ssh_server.example.com` but not directly from your local machine) via your `localhost:5432`.
        ```bash
        ssh -L 5432:db.internal.example.com:5432 jdoe@ssh_server.example.com
        # Now connect your local DB client to localhost:5432
        ```
    *   The `<remote_destination_host>` is resolved from the perspective of the `<ssh_server_host>`.
*   **Remote Port Forwarding (`-R`)**: Expose a local service to a remote network.
    `ssh -R <remote_port_to_listen_on_ssh_server>:<local_host_to_forward_to>:<local_port_to_forward_to> <username>@<ssh_server_host>`
    *   Example: Make your local web server running on `localhost:8080` accessible on `ssh_server.example.com:9090`.
        ```bash
        ssh -R 9090:localhost:8080 jdoe@ssh_server.example.com
        # Anyone who can access ssh_server.example.com:9090 will be forwarded to your localhost:8080.
        # By default, the remote port might only listen on the loopback interface of the ssh_server.
        # To make it listen on all interfaces on the server, you might need GatewayPorts yes in sshd_config on the server, or specify the bind_address:
        # ssh -R 0.0.0.0:9090:localhost:8080 user@ssh_server
        ```
*   **Dynamic Port Forwarding (SOCKS Proxy) (`-D`)**: Create a SOCKS proxy through the SSH server.
    `ssh -D <local_socks_proxy_port> <username>@<ssh_server_host>`
    *   Example: Create a SOCKS proxy on your `localhost:1080` that tunnels traffic through `ssh_server.example.com`.
        ```bash
        ssh -D 1080 jdoe@ssh_server.example.com
        # Configure your browser or applications to use SOCKS5 proxy at localhost:1080.
        ```
*   **Backgrounding tunnels**: Add `-fN` to send SSH to the background and not execute a remote command.
    ```bash
    ssh -fN -L 8080:localhost:80 user@remote_server
    ```

## Server-Side Configuration (`/etc/ssh/sshd_config` on the server)

Common options to consider for hardening:
*   `Port 22`: Change to a non-standard port (minor obscurity, not true security).
*   `PermitRootLogin no`: Disallow root login via SSH.
*   `PasswordAuthentication no`: Disable password authentication (force key-based auth).
*   `PubkeyAuthentication yes`: Ensure public key authentication is enabled.
*   `AuthorizedKeysFile .ssh/authorized_keys`: Path to authorized keys file.
*   `AllowUsers user1 user2`: Whitelist specific users.
*   `AllowGroups ssh_users`: Whitelist specific groups.
*   `ChallengeResponseAuthentication no`: Disable challenge-response authentication.
*   `UsePAM yes` (often default): Pluggable Authentication Modules.
*   `X11Forwarding no`: Disable X11 forwarding if not needed.
*   `ClientAliveInterval 300`
*   `ClientAliveCountMax 0` (or a small number like 3)
*   `MaxAuthTries 3`
*   `LoginGraceTime 30s`
*   `Subsystem sftp /usr/lib/openssh/sftp-server` (ensure SFTP is configured)

Remember to restart the SSH daemon after changes: `sudo systemctl restart sshd` or `sudo service ssh restart`.

## Troubleshooting

*   Use `-v`, `-vv`, or `-vvv` for verbose output to diagnose connection problems.
*   Check file permissions on the server for `~/.ssh` (should be `700`) and `~/.ssh/authorized_keys` (should be `600`).
*   Check server logs (e.g., `/var/log/auth.log` or `/var/log/secure`).
*   Ensure the firewall on the server is not blocking the SSH port.
*   Verify `sshd` service is running on the server.

This provides a much more detailed and actionable cheatsheet for SSH. I'll proceed with `firewall_ufw_iptables.md` next.The `ssh.md` cheatsheet has been successfully updated with detailed command examples for various SSH functionalities, including public key authentication, SSH agent usage, file transfer, and tunneling, all formatted as requested.

Next, I will enhance `firewall_ufw_iptables.md` by providing more specific command examples for both UFW and iptables, covering common scenarios for managing firewall rules.
