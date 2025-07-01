# SSH (Secure Shell) Cheatsheet

*   **Purpose**: Secure remote login, command execution, file transfer.
*   **Key Concepts**: Client-server model, encryption.
*   **Authentication Methods**:
    *   Password-based (less secure, often disabled).
    *   Public Key Authentication (more secure, recommended):
        *   Generate key pair: `ssh-keygen -t rsa -b 4096` (or `ed25519`). Creates `id_rsa` (private) and `id_rsa.pub` (public).
        *   Copy public key to server: `ssh-copy-id user@host` or manually add to `~/.ssh/authorized_keys` on server.
*   **Connecting**: `ssh user@hostname -p port_number` (default port is 22).
*   **Configuration File (`~/.ssh/config` on client)**:
    ```
    Host myserver
        HostName server.example.com
        User myuser
        Port 2222
        IdentityFile ~/.ssh/my_custom_key
    ```
*   **Tunneling (Port Forwarding)**:
    *   Local Port Forwarding: `ssh -L local_port:destination_host:destination_port user@ssh_server_host` (Access `destination_host:destination_port` via `localhost:local_port`).
    *   Remote Port Forwarding: `ssh -R remote_port:local_host:local_port user@ssh_server_host` (Access `local_host:local_port` on client via `ssh_server_host:remote_port`).
    *   Dynamic Port Forwarding (SOCKS proxy): `ssh -D local_port user@ssh_server_host`.
*   **File Transfer**:
    *   `scp`: `scp source_file user@host:destination_path` or `scp user@host:source_file destination_path`.
    *   `sftp`: Interactive file transfer program.
*   **`sshd_config` (Server configuration, usually `/etc/ssh/sshd_config`)**: Hardening options (e.g., `PasswordAuthentication no`, `PermitRootLogin no`, `AllowUsers`).
*   **Agent Forwarding**: `ssh -A user@host` (use with caution, allows remote host to use your local SSH keys).
