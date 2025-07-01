# Cron Jobs Cheatsheet

*   **Purpose**: Scheduling commands or scripts to run periodically.
*   **Crontab File**: User-specific (`crontab -e`), system-wide (`/etc/crontab`, `/etc/cron.d/`).
*   **Timing Syntax (5 fields + command)**:
    *   Minute (0-59)
    *   Hour (0-23)
    *   Day of Month (1-31)
    *   Month (1-12 or JAN-DEC)
    *   Day of Week (0-7 or SUN-SAT, where 0 and 7 are Sunday)
*   **Special Characters**:
    *   `*`: Any value.
    *   `,`: Value list separator.
    *   `-`: Range of values.
    *   `/`: Step values (e.g., `*/15` for every 15 minutes).
*   **Special Strings (Macros)**: `@reboot`, `@yearly`, `@annually`, `@monthly`, `@weekly`, `@daily`, `@hourly`.
*   **Real Examples**:
    *   Run a script every day at 2 AM: `0 2 * * * /path/to/script.sh`
    *   Run a command every 15 minutes: `*/15 * * * * /usr/bin/some_command`
    *   Run a script on the 1st of every month at midnight: `0 0 1 * * /path/to/monthly_report.sh`
    *   Run a script every Monday at 9 AM: `0 9 * * 1 /path/to/weekly_task.sh`
*   **Managing Cron Jobs**: `crontab -l` (list), `crontab -r` (remove).
*   **Environment**: Cron jobs run with a minimal environment; specify full paths to executables, manage `PATH` if needed.
*   **Logging Output**: Redirect stdout and stderr (`> /path/to/logfile.log 2>&1`).
