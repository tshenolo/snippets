# VSCode (Visual Studio Code) Cheatsheet

Visual Studio Code is a popular, free source code editor developed by Microsoft. This cheatsheet covers common shortcuts, features, and settings.

## General Interface & Command Palette

*   **Command Palette**: The primary way to access all commands in VSCode.
    *   `Ctrl+Shift+P` or `Cmd+Shift+P` (macOS) or `F1`
    *   Type `>` to see and run commands.
    *   Examples: `>File: Save`, `>Git: Commit`, `>Preferences: Open Settings (UI)`
*   **Quick Open (Go to File)**: Quickly open files by name.
    *   `Ctrl+P` or `Cmd+P` (macOS)
    *   Type filename. Use `@` for symbols, `#` for workspace symbols, `:` for line numbers (e.g., `myfile.js:10`).
*   **Toggle Sidebar Visibility**:
    *   `Ctrl+B` or `Cmd+B` (macOS)
*   **Toggle Panel Visibility** (Terminal, Output, Debug Console, Problems):
    *   `Ctrl+J` or `Cmd+J` (macOS) (Toggles the whole panel)
    *   `Ctrl+\`` or `Cmd+\`` (macOS) (Specifically toggles the integrated terminal)
*   **Zen Mode** (Distraction-free view):
    *   `Ctrl+K Z` (Press `Ctrl+K` then `Z`) or `Cmd+K Z` (macOS)
    *   Press `Esc` twice to exit.
*   **Split Editor**:
    *   `Ctrl+\` or `Cmd+\` (macOS) (Splits editor vertically) - *Note: This might conflict with Toggle Terminal, check your keybindings.*
    *   Alternatively, use Command Palette: `>View: Split Editor Right/Down`
    *   Focus on editor groups: `Ctrl+1`, `Ctrl+2`, etc. or `Cmd+1`, `Cmd+2` (macOS)
*   **Switch between open files/editors**:
    *   `Ctrl+Tab` or `Cmd+Tab` (macOS) (Cycles through recently used)
    *   `Ctrl+PageDown`/`Ctrl+PageUp` or `Cmd+Option+RightArrow`/`Cmd+Option+LeftArrow` (macOS)

## Editing Text

*   **Basic Editing**: Standard shortcuts like `Ctrl+C` (Copy), `Ctrl+X` (Cut), `Ctrl+V` (Paste), `Ctrl+Z` (Undo), `Ctrl+Y` or `Ctrl+Shift+Z` (Redo).
*   **Multi-Cursor Editing**:
    *   `Alt+Click` (Windows/Linux) or `Option+Click` (macOS): Add cursor at click location.
    *   `Ctrl+Alt+DownArrow` / `Ctrl+Alt+UpArrow` (Windows/Linux) or `Cmd+Option+DownArrow` / `Cmd+Option+UpArrow` (macOS): Insert cursor below/above.
    *   `Ctrl+D` or `Cmd+D` (macOS): Select next occurrence of current selection (adds another cursor).
    *   `Ctrl+Shift+L` or `Cmd+Shift+L` (macOS): Select all occurrences of current selection.
*   **Line Operations**:
    *   `Ctrl+Enter` or `Cmd+Enter` (macOS): Insert line below.
    *   `Ctrl+Shift+Enter` or `Cmd+Shift+Enter` (macOS): Insert line above.
    *   `Alt+UpArrow` / `Alt+DownArrow` (Windows/Linux) or `Option+UpArrow` / `Option+DownArrow` (macOS): Move line up/down.
    *   `Shift+Alt+UpArrow` / `Shift+Alt+DownArrow` (Windows/Linux) or `Shift+Option+UpArrow` / `Shift+Option+DownArrow` (macOS): Copy line up/down.
    *   `Ctrl+Shift+K` or `Cmd+Shift+K` (macOS): Delete current line.
    *   `Ctrl+X` (with no selection) or `Cmd+X` (macOS): Cut current line.
    *   `Ctrl+/` or `Cmd+/` (macOS): Toggle line comment.
    *   `Shift+Alt+A` or `Shift+Option+A` (macOS): Toggle block comment.
*   **Indentation**:
    *   `Tab`: Indent selection (or current line).
    *   `Shift+Tab`: Outdent selection (or current line).
    *   `Ctrl+]` / `Ctrl+[` or `Cmd+]` / `Cmd+[` (macOS): Indent/Outdent line.
*   **Code Folding**:
    *   `Ctrl+Shift+[` or `Cmd+Option+[` (macOS): Fold region.
    *   `Ctrl+Shift+]` or `Cmd+Option+]` (macOS): Unfold region.
    *   `Ctrl+K Ctrl+0` or `Cmd+K Cmd+0` (macOS): Fold all regions.
    *   `Ctrl+K Ctrl+J` or `Cmd+K Cmd+J` (macOS): Unfold all regions.
*   **Format Document**:
    *   `Shift+Alt+F` or `Shift+Option+F` (macOS)
    *   Or via Command Palette: `>Format Document` (Requires a formatter extension for the language).
*   **Go to Definition**:
    *   `F12` or `Ctrl+Click` (`Cmd+Click` on macOS) on a symbol.
*   **Peek Definition**:
    *   `Alt+F12` or `Option+F12` (macOS). Shows definition in an inline window.
*   **Find References**:
    *   `Shift+F12`.
*   **Rename Symbol**:
    *   `F2`. Renames symbol across files.

## Navigation

*   **Go to Line**: `Ctrl+G`, then type line number.
*   **Go to Symbol in File**: `Ctrl+Shift+O` or `Cmd+Shift+O` (macOS).
*   **Go to Symbol in Workspace**: `Ctrl+T` or `Cmd+T` (macOS).
*   **Navigate Back/Forward** (editor navigation history):
    *   `Alt+LeftArrow` / `Alt+RightArrow` (Windows/Linux)
    *   `Ctrl+-` / `Ctrl+Shift+-` (Windows/Linux)
    *   `Cmd+Option+LeftArrow` / `Cmd+Option+RightArrow` or `Ctrl+-` / `Ctrl+Shift+-` (macOS)
*   **Scroll**:
    *   `Ctrl+UpArrow`/`DownArrow`: Scroll line up/down.
    *   `Alt+PageUp`/`PageDown`: Scroll page up/down.

## Search and Replace

*   **Find in Current File**:
    *   `Ctrl+F` or `Cmd+F` (macOS)
    *   Options: Match Case (`Alt+C` or `Cmd+Option+C`), Match Whole Word (`Alt+W` or `Cmd+Option+W`), Use Regular Expression (`Alt+R` or `Cmd+Option+R`).
*   **Replace in Current File**:
    *   `Ctrl+H` or `Cmd+Option+F` (macOS)
*   **Find in Files (Workspace Search)**:
    *   `Ctrl+Shift+F` or `Cmd+Shift+F` (macOS)
*   **Replace in Files**:
    *   `Ctrl+Shift+H` or `Cmd+Shift+H` (macOS)

## Integrated Terminal

*   **Open New Terminal**:
    *   `Ctrl+\`` or `Cmd+\`` (macOS) (Toggles existing or opens new)
    *   Or via Command Palette: `>Terminal: Create New Integrated Terminal`
*   **Split Terminal**: Click the split icon in the terminal panel or `Ctrl+Shift+5` (`Cmd+Shift+5` on macOS).
*   **Focus Terminal**: `Ctrl+\`` (if already open).
*   **Kill Terminal**: Click the trash icon or type `exit`.

## Extensions

VSCode's power comes from its vast extension ecosystem.
*   **Browse and Install Extensions**:
    *   `Ctrl+Shift+X` or `Cmd+Shift+X` (macOS) (Opens Extensions view in sidebar)
    *   Search for extensions (e.g., "Python", "Prettier", "ESLint", "Live Server", "Docker", "Remote - SSH").
*   **Recommended Extensions (Examples)**:
    *   **Language Support**: Python, JavaScript ES6 Snippets, Java Extension Pack, PHP IntelliSense.
    *   **Linters & Formatters**: ESLint, Prettier - Code formatter, Pylint, Beautify.
    *   **Git**: GitLens (powerful Git history and blame), Git Graph.
    *   **Productivity**: Live Server (launch local dev server with live reload), Path Intellisense, TODO Highlight.
    *   **Themes & Icons**: Material Icon Theme, One Dark Pro.
    *   **Remote Development**: Remote - SSH, Remote - Containers, WSL (for Windows Subsystem for Linux).

## Source Control (Git Integration)

VSCode has excellent built-in Git support.
*   **Open Source Control View**: `Ctrl+Shift+G` or `Cmd+Shift+G` (macOS).
*   **Initialize Repository**: If project is not yet a Git repo.
*   **Stage Changes**: Click `+` icon next to files or use Command Palette `>Git: Stage`.
*   **Unstage Changes**: Click `-` icon.
*   **Commit Changes**: Enter commit message and click checkmark icon or `Ctrl+Enter` (`Cmd+Enter` on macOS).
*   **Push, Pull, Sync**: Available via `...` menu in Source Control view or Command Palette.
    *   `>Git: Push`
    *   `>Git: Pull`
    *   `>Git: Sync` (Pulls then Pushes)
*   **Branching & Merging**:
    *   Create Branch: `>Git: Create Branch`
    *   Checkout Branch: Click current branch name in status bar or `>Git: Checkout to...`
    *   Merge Branch: `>Git: Merge Branch...`
*   **View Diffs**: Click on a changed file in Source Control view.

## Debugging

VSCode has a built-in debugger.
*   **Open Debug View**: `Ctrl+Shift+D` or `Cmd+Shift+D` (macOS).
*   **Start Debugging**: `F5`.
*   **Set Breakpoints**: Click in the gutter to the left of line numbers.
*   **Debug Controls**: Step Over (`F10`), Step Into (`F11`), Step Out (`Shift+F11`), Continue (`F5`), Restart, Stop.
*   **Configuration (`launch.json`)**: Click the gear icon in Debug view to create/edit `launch.json` for specific debug configurations (e.g., for Node.js, Python, browsers).
    ```json
    // .vscode/launch.json example for Node.js
    {
      "version": "0.2.0",
      "configurations": [
        {
          "type": "node",
          "request": "launch",
          "name": "Launch Program",
          "skipFiles": ["<node_internals>/**"],
          "program": "${workspaceFolder}/app.js" // Your main entry file
        }
      ]
    }
    ```

## Settings (`settings.json`)

Customize VSCode to your liking.
*   **Open Settings UI**: `Ctrl+,` or `Cmd+,` (macOS) or `>Preferences: Open Settings (UI)`.
*   **Open `settings.json` file**: `>Preferences: Open User Settings (JSON)` or `>Preferences: Open Workspace Settings (JSON)`.
*   **User Settings**: Apply globally to all VSCode instances.
*   **Workspace Settings**: Specific to the current project/workspace (stored in `.vscode/settings.json`). Overrides user settings.
*   **Common Settings Examples**:
    ```jsonc
    // settings.json
    {
      "editor.fontSize": 14,
      "editor.fontFamily": "Fira Code, Menlo, Monaco, 'Courier New', monospace",
      "editor.fontLigatures": true, // For fonts like Fira Code
      "editor.tabSize": 2,
      "editor.insertSpaces": true, // Use spaces instead of tabs
      "editor.wordWrap": "on",
      "files.autoSave": "onFocusChange", // Or "afterDelay", "off"
      "workbench.colorTheme": "Default Dark+", // Or your preferred theme
      "workbench.iconTheme": "material-icon-theme", // If Material Icon Theme is installed
      "terminal.integrated.fontSize": 13,
      "explorer.confirmDragAndDrop": false,
      // Language-specific settings
      "[python]": {
        "editor.defaultFormatter": "ms-python.python", // If Python extension is installed
        "editor.formatOnSave": true,
        "editor.tabSize": 4
      },
      "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode", // If Prettier is installed
        "editor.formatOnSave": true
      },
      "prettier.singleQuote": true, // Example Prettier setting
      "files.associations": { // Associate file patterns with languages
          "*.module": "php"
      }
    }
    ```

## Tasks (`tasks.json`)

Automate common development tasks like building, testing, linting.
*   **Configure Tasks**: `>Tasks: Configure Task` or create/edit `.vscode/tasks.json`.
    ```jsonc
    // .vscode/tasks.json example for running a build script
    {
      "version": "2.0.0",
      "tasks": [
        {
          "label": "Build Project",
          "type": "npm", // Or "shell", "process"
          "script": "build", // Your npm script name from package.json
          "group": {
            "kind": "build",
            "isDefault": true
          },
          "problemMatcher": [
            "$tsc" // Example problem matcher for TypeScript
          ]
        },
        {
          "label": "Run Tests",
          "type": "npm",
          "script": "test",
          "group": "test"
        }
      ]
    }
    ```
*   **Run Task**: `>Tasks: Run Task` (then select the task).
*   **Run Build Task**: `Ctrl+Shift+B` or `Cmd+Shift+B` (macOS) (runs the default build task).

## Snippets

Define custom code snippets for faster coding.
*   **Configure User Snippets**: `>Preferences: Configure User Snippets`. Select language or create global snippets.
    ```jsonc
    // Example: javascript.json (User Snippets)
    {
      "Console Log": {
        "prefix": "clog", // Type 'clog' and press Tab
        "body": [
          "console.log('$1');",
          "$2"
        ],
        "description": "Log output to console"
      },
      "For Loop": {
        "prefix": "forloop",
        "body": [
          "for (let ${1:i} = 0; ${1:i} < ${2:array}.length; ${1:i}++) {",
          "\tconst ${3:element} = ${2:array}[${1:i}];",
          "\t$0",
          "}"
        ],
        "description": "For loop"
      }
    }
    // $1, $2 are tab stops. $0 is the final cursor position.
    // ${1:i} is a tab stop with a placeholder.
    ```

