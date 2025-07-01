# tmux (Terminal Multiplexer) Cheatsheet

*   **Purpose**: Manage multiple terminal sessions, windows, and panes within a single terminal window. Sessions persist even if you disconnect.
*   **Key Concepts**:
    *   Server: Background process managing sessions.
    *   Session: A collection of windows.
    *   Window: A single screen, can be split into panes.
    *   Pane: A rectangular part of a window running a separate shell.
*   **Prefix Key**: Default is `Ctrl+b`. Commands are issued by `Prefix` then `key`.
*   **Sessions**:
    *   Start new session: `tmux new -s session_name`.
    *   List sessions: `tmux ls`.
    *   Attach to session: `tmux attach -t session_name` or `tmux a -t session_name`.
    *   Detach from session: `Prefix` `d`.
    *   Kill session: `tmux kill-session -t session_name`.
*   **Windows (within a session)**:
    *   Create new window: `Prefix` `c`.
    *   Next window: `Prefix` `n`.
    *   Previous window: `Prefix` `p`.
    *   Go to window by number: `Prefix` `0-9`.
    *   Rename window: `Prefix` `,`.
    *   Close window: `Prefix` `&`.
*   **Panes (within a window)**:
    *   Split horizontally: `Prefix` `%`.
    *   Split vertically: `Prefix` `"`.
    *   Navigate panes: `Prefix` `arrow_keys`.
    *   Close pane: `Prefix` `x` (or `exit` in shell).
    *   Zoom pane: `Prefix` `z` (toggle).
    *   Swap panes: `Prefix` `{` (previous), `Prefix` `}` (next).
    *   Resize panes: `Prefix` `Ctrl+arrow_keys` (hold Ctrl).
*   **Scrolling (Copy Mode)**: `Prefix` `[` then use arrow keys/PageUp/PageDown. `q` to exit copy mode.
*   **Configuration**: `~/.tmux.conf`.
