# Ansible Cheatsheet

*   **Core Concepts**: Agentless automation, idempotent, declarative language (YAML).
*   **Components**:
    *   Control Node: Machine where Ansible is installed and run.
    *   Managed Nodes (Hosts): Servers being managed.
    *   Inventory: File (INI or YAML) defining managed nodes, groups, and variables.
    *   Playbooks: YAML files defining a set of plays to run.
    *   Plays: A set of tasks run against a group of hosts.
    *   Tasks: Units of action, typically calling a module.
    *   Modules: Reusable scripts that perform specific actions (e.g., `apt`, `yum`, `copy`, `service`, `user`).
    *   Roles: Way to organize playbooks into reusable structures.
    *   Handlers: Tasks triggered by `notify` directives, typically run at the end of a play.
    *   Variables: Used for customization (defined in inventory, playbooks, roles, etc.).
*   **Inventory File (`inventory.ini` or `inventory.yml`)**:
    *   Example (INI):
        ```ini
        [webservers]
        web1.example.com
        web2.example.com ansible_user=ubuntu
        [dbservers]
        db1.example.com
        ```
*   **Playbook Structure (YAML)**:
    ```yaml
    ---
    - name: Configure web servers
      hosts: webservers
      become: yes # Equivalent to sudo
      tasks:
        - name: Install nginx
          ansible.builtin.apt: # or yum for RHEL-based
            name: nginx
            state: present
        - name: Ensure nginx is running and enabled
          ansible.builtin.service:
            name: nginx
            state: started
            enabled: yes
        - name: Copy nginx config
          ansible.builtin.copy:
            src: files/nginx.conf
            dest: /etc/nginx/nginx.conf
          notify: Restart nginx
      handlers:
        - name: Restart nginx
          ansible.builtin.service:
            name: nginx
            state: restarted
    ```
*   **Common Modules**:
    *   Package Management: `apt`, `yum`, `dnf`, `pacman`, `pip`.
    *   File Management: `copy`, `template`, `file`, `lineinfile`, `blockinfile`, `fetch`.
    *   Service Management: `service`, `systemd`.
    *   User Management: `user`, `group`.
    *   Command Execution: `command`, `shell`, `script`.
    *   Source Control: `git`.
*   **Running Playbooks**: `ansible-playbook -i <inventory_file> <playbook.yml>`.
*   **Ad-hoc Commands**: `ansible <host-pattern> -m <module> -a "<args>"`.
*   **Ansible Vault**: Encrypting sensitive data.
