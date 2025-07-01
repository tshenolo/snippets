# Bash Cheatsheet

*   **Basic Commands**: `ls`, `cd`, `pwd`, `mkdir`, `rm`, `cp`, `mv`, `cat`, `echo`, `grep`, `find`, `chmod`, `chown`.
*   **Variables**: Declaration (`VAR="value"`), usage (`$VAR` or `${VAR}`).
*   **Command Substitution**: `$(command)` or `` `command` ``.
*   **Arithmetic Expansion**: `$((expression))`.
*   **Input/Output Redirection**: `>`, `>>`, `<`, `2>`, `&>`, `|` (pipes).
*   **Loops**:
    *   `for var in list; do ... done`
    *   `for (( expr1; expr2; expr3 )); do ... done` (C-style)
    *   `while condition; do ... done`
    *   `until condition; do ... done`
*   **Conditionals**:
    *   `if condition; then ... elif condition; then ... else ... fi`
    *   Test command (`[ expression ]` or `[[ expression ]]`): File tests (`-f`, `-d`), string comparisons (`=`, `!=`, `-z`, `-n`), numerical comparisons (`-eq`, `-ne`, `-lt`, `-gt`).
    *   `case` statements.
*   **Functions**: `function_name() { commands; }` or `function function_name { commands; }`, arguments (`$1`, `$2`, `$@`, `$*`), return status (`return code`).
*   **File Operations**: Reading line by line, checking existence, permissions.
*   **Scripting Best Practices**: Shebang (`#!/bin/bash`), comments, error handling (`set -e`, `set -u`, `set -o pipefail`), exit codes.
