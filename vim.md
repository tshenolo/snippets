# Vim Cheatsheet

This document provides a comprehensive cheatsheet for Vim commands, organized by category.

## Table of Contents

* [Navigation](#navigation)
* [Editing](#editing)
* [Visual Mode](#visual-mode)
* [Command-Line Mode](#command-line-mode)
* [File Operations](#file-operations)
* [Search and Replace](#search-and-replace)
* [Buffers and Windows](#buffers-and-windows)
* [Marks and Jumps](#marks-and-jumps)
* [Macros](#macros)
* [Miscellaneous](#miscellaneous)

## Navigation

### Basic Movement
* `h`: Move cursor left
* `j`: Move cursor down
* `k`: Move cursor up
* `l`: Move cursor right

### Word Movement
* `w`: Move to the start of the next word
* `W`: Move to the start of the next WORD (ignores punctuation)
* `b`: Move to the start of the previous word
* `B`: Move to the start of the previous WORD (ignores punctuation)
* `e`: Move to the end of the current word
* `E`: Move to the end of the current WORD (ignores punctuation)

### Line Movement
* `0` (zero): Move to the beginning of the line (first character)
* `^`: Move to the first non-blank character of the line
* `$`: Move to the end of the line
* `g_`: Move to the last non-blank character of the line

### Screen Movement
* `H`: Move to the top of the screen (High)
* `M`: Move to the middle of the screen (Middle)
* `L`: Move to the bottom of the screen (Low)
* `Ctrl+u`: Scroll up half a page (Up)
* `Ctrl+d`: Scroll down half a page (Down)
* `Ctrl+f`: Scroll forward one full page
* `Ctrl+b`: Scroll backward one full page
* `Ctrl+e`: Scroll screen down one line
* `Ctrl+y`: Scroll screen up one line
* `zt`: Scroll screen to make current line appear at the top
* `zz`: Scroll screen to make current line appear at the center
* `zb`: Scroll screen to make current line appear at the bottom

### File Movement
* `gg`: Go to the first line of the file
* `G`: Go to the last line of the file
* `:<line_number>` or `<line_number>G`: Go to a specific line number
* `:%`: Go to a specific percentage of the file (e.g., `50%`)

### Jumping
* `Ctrl+o`: Go to older cursor position (jump back)
* `Ctrl+i` or `Tab`: Go to newer cursor position (jump forward)
* `''` (two single quotes): Go to the position before the last jump
* `` ` `` (backtick) + mark: Go to a mark (see [Marks and Jumps](#marks-and-jumps))

## Editing

### Entering Insert Mode
* `i`: Insert text before the cursor
* `I`: Insert text at the beginning of the line
* `a`: Append text after the cursor
* `A`: Append text at the end of the line
* `o`: Open a new line below the current line and enter insert mode
* `O`: Open a new line above the current line and enter insert mode
* `s`: Substitute character under cursor and enter insert mode
* `S`: Substitute entire line and enter insert mode
* `cc`: Change (replace) entire line and enter insert mode
* `c<motion>`: Change text covered by `<motion>` (e.g., `cw` to change word)

### Deleting Text (Normal Mode)
* `x`: Delete character under the cursor
* `X`: Delete character before the cursor
* `dw`: Delete word from cursor
* `db`: Delete word backward from cursor
* `dd`: Delete the current line
* `d<motion>`: Delete text covered by `<motion>` (e.g., `d$` to delete to end of line, `dG` to delete to end of file)
* `D`: Delete from cursor to the end of the line (same as `d$`)

### Changing Text (Normal Mode)
* `r<char>`: Replace character under cursor with `<char>`
* `R`: Enter replace mode (overwrite characters)
* `~`: Toggle case of character under cursor
* `.` (dot): Repeat the last change

### Yanking (Copying) and Pasting
* `yy` or `Y`: Yank (copy) the current line
* `y<motion>`: Yank text covered by `<motion>` (e.g., `yw` to yank word)
* `p`: Paste after the cursor or current line
* `P`: Paste before the cursor or current line
* `gp`: Paste after the cursor/line and move cursor to end of pasted text
* `gP`: Paste before the cursor/line and move cursor to end of pasted text
* `ddp`: Swap current line with the line below
* `ddkP`: Swap current line with the line above

### Undo and Redo
* `u`: Undo last change
* `U`: Undo all changes on the current line
* `Ctrl+r`: Redo last undone change

### Indentation
* `>>`: Indent current line
* `<<`: Unindent current line
* `>` or `<` in Visual Mode: Indent or unindent selected lines
* `=`: Auto-indent (e.g., `gg=G` to auto-indent entire file, requires filetype plugin or `cindent`/`smartindent`)

## Visual Mode

* `v`: Enter visual mode (character-wise selection)
* `V`: Enter visual line mode (line-wise selection)
* `Ctrl+v`: Enter visual block mode (block-wise selection)
* `o`: In visual mode, move cursor to the other end of the selection
* `Esc` or `Ctrl+c`: Exit visual mode

### Actions in Visual Mode
Once text is selected:
* `d` or `x`: Delete selected text
* `y`: Yank (copy) selected text
* `c`: Change selected text
* `s`: Substitute selected text
* `r<char>`: Replace all selected characters with `<char>` (character-wise visual mode)
* `~`: Toggle case of selected text
* `>`: Indent selected lines
* `<`: Unindent selected lines
* `J`: Join selected lines
* `gq`: Format selected lines (e.g., to textwidth)
* `:w <filename>`: Save selected lines to a new file
* `:'<,'>! <command>`: Filter selected lines through an external command

## Command-Line Mode

Press `:` to enter command-line mode.

### Basic Commands
* `:w`: Write (save) the file
* `:w <filename>`: Write to a new file `<filename>`
* `:wq` or `:x` or `ZZ`: Write and quit
* `:q`: Quit (fails if there are unsaved changes)
* `:q!`: Quit without saving (discard changes)
* `:qa`: Quit all open files
* `:qa!`: Quit all open files without saving
* `:e <filename>`: Edit a file
* `:e!`: Revert to the last saved version of the current file
* `:ls`: List open buffers
* `:bn`: Go to the next buffer
* `:bp`: Go to the previous buffer
* `:bd`: Delete (close) current buffer
* `:sp <filename>`: Split window horizontally and open `<filename>`
* `:vsp <filename>`: Split window vertically and open `<filename>`
* `:new`: Open a new empty window horizontally
* `:vnew`: Open a new empty window vertically
* `:set <option>`: Set an option (e.g., `:set number` to show line numbers)
* `:set <option>?`: View current value of an option
* `:set <option>!` : Toggle boolean option
* `:set all`: Show all option values
* `:help <topic>`: Open help for `<topic>` (e.g., `:help :w`)
* `:!<command>`: Execute an external shell command (e.g., `:!ls -l`)
* `:shell`: Start a shell
* `:read <filename>`: Insert content of `<filename>` below current line
* `:write <filename>`: Write current file to `<filename>`
* `:source <filename>`: Execute Vim script in `<filename>`

### Ranges
Many commands can take a range.
* `:<start_line>,<end_line> <command>`: Execute command on lines from `<start_line>` to `<end_line>`
* `:% <command>`: Execute command on all lines
* `:. <command>`: Execute command on the current line
* `:'<,'> <command>`: Execute command on visually selected lines (Vim fills this automatically)
* `:/pattern/ <command>`: Execute command on the next line matching `pattern`
* `:/pattern1/,/pattern2/ <command>`: Execute command on lines between `pattern1` and `pattern2`

## File Operations

* `:w`: Save current file
* `:saveas <filepath>`: Save current file to a new path
* `:Explore` or `:E`: Open file explorer (netrw) in current window
* `:Sex`: Open file explorer in a horizontal split
* `:Vex`: Open file explorer in a vertical split
* `:cd <directory>`: Change current directory
* `:pwd`: Print working directory
* `:mkdir <directory_name>`: Create a directory (Vim 8+)
* `:!mkdir -p <directory_name>`: Create directory (older Vim, or if nested)

## Search and Replace

### Searching
* `/pattern`: Search forward for `pattern`
* `?pattern`: Search backward for `pattern`
* `n`: Repeat last search in the same direction
* `N`: Repeat last search in the opposite direction
* `*`: Search forward for the word under the cursor
* `#`: Search backward for the word under the cursor
* `g*`: Search forward for the current partial word under the cursor
* `g#`: Search backward for the current partial word under the cursor
* `:set hlsearch` or `:set hls`: Highlight all search matches
* `:set nohlsearch` or `:set nohls`: Disable search highlighting
* `:nohlsearch` or `:noh`: Clear current search highlighting (until next search)
* `:set incsearch` or `:set is`: Show matches incrementally while typing search pattern
* `:set ignorecase` or `:set ic`: Ignore case in searches
* `:set smartcase` or `:set scs`: Ignore case unless pattern contains uppercase letters

### Replacing
* `:[range]s/old/new/[flags]`: Substitute `old` with `new`
    * `range`: e.g., `%` for whole file, `.` for current line, `'<,'>` for visual selection. Default is current line.
    * `flags`:
        * `g`: Global (replace all occurrences in the line, not just the first)
        * `c`: Confirm each replacement
        * `i`: Ignore case for `old` pattern
        * `I`: Case-sensitive for `old` pattern
        * `n`: Report number of matches, but don't substitute
* `:%s/old/new/g`: Replace all occurrences of `old` with `new` in the entire file
* `:'<,'>s/old/new/gc`: Replace all occurrences in visual selection, with confirmation

## Buffers and Windows

### Buffers (Files in memory)
* `:ls` or `:buffers`: List all open buffers
* `:b <buffer_number_or_name>`: Switch to buffer (e.g., `:b 3` or `:b filename.txt`)
* `:bn` or `:bnext`: Go to the next buffer
* `:bp` or `:bprevious`: Go to the previous buffer
* `:bf` or `:bfirst`: Go to the first buffer
* `:bl` or `:blast`: Go to the last buffer
* `:bd` or `:bdelete`: Close (delete) current buffer. If unsaved, will fail unless `!` is added (`:bd!`).
* `:bw` or `:bwipeout`: Completely wipe out the buffer (cannot be undone easily).
* `:bufdo <command>`: Execute `<command>` on all listed buffers.

### Windows (Viewports into buffers)
* `Ctrl+w s` or `:sp[lit]`: Split current window horizontally
* `Ctrl+w v` or `:vs[plit]`: Split current window vertically
* `Ctrl+w n` or `:new`: Create a new empty window (horizontal split)
* `Ctrl+w q` or `:q[uit]` or `:cl[ose]`: Close current window
* `Ctrl+w o` or `:on[ly]`: Close all other windows (keep only current)
* `Ctrl+w c`: Close current window (same as `:close`)
* `Ctrl+w =`: Make all windows equal size
* `Ctrl+w _`: Maximize current window height
* `Ctrl+w |`: Maximize current window width
* `Ctrl+w <number> +`: Increase window height by `<number>` lines
* `Ctrl+w <number> -`: Decrease window height by `<number>` lines
* `Ctrl+w <number> >`: Increase window width by `<number>` columns
* `Ctrl+w <number> <`: Decrease window width by `<number>` columns
* `Ctrl+w h/j/k/l`: Move cursor to window left/down/up/right
* `Ctrl+w H/J/K/L`: Move current window to far left/bottom/top/right
* `Ctrl+w r`: Rotate windows right/down
* `Ctrl+w R`: Rotate windows left/up
* `Ctrl+w p`: Go to previous (last accessed) window
* `Ctrl+w t`: Move current window to a new tab
* `:windo <command>`: Execute `<command>` on all windows.

### Tabs
* `:tabnew <filename>`: Open `<filename>` in a new tab
* `:tabnew`: Open a new empty tab
* `:tabclose` or `:tabc`: Close current tab
* `:tabonly` or `:tabo`: Close all other tabs
* `gt` or `:tabn[ext]`: Go to the next tab
* `gT` or `:tabp[revious]`: Go to the previous tab
* `<N>gt`: Go to tab number `N` (e.g., `3gt` for 3rd tab)
* `:tabm <N>`: Move current tab to position `N` (0-indexed)

## Marks and Jumps

* `m<letter>`: Set a mark named `<letter>` (lowercase for current file, uppercase for global/across files) at cursor position.
    * e.g., `ma` sets mark 'a'
* `` ` ``<letter>``: Go to the exact position of mark `<letter>`.
    * e.g., `` `a `` goes to mark 'a'
* `'<letter>`: Go to the beginning of the line containing mark `<letter>`.
    * e.g., `'a` goes to the line of mark 'a'
* `` ` ``.``: Go to the position where the last change was made.
* `'.`: Go to the line where the last change was made.
* `` ` ``^``: Go to the position where insert mode was last exited.
* `` ` ``{``: Go to previous paragraph start.
* `` ` ``}``: Go to next paragraph start.
* `` ` ``[``: Go to previous `[` character.
* `` ` ``]``: Go to next `]` character.
* `:marks`: List all current marks.
* `:delmarks <marks>`: Delete specified marks (e.g., `:delmarks a b c`)
* `:delmarks!`: Delete all lowercase marks for the current buffer.

## Macros

* `q<letter>`: Start recording a macro into register `<letter>` (e.g., `qa`).
* `q`: Stop recording the macro (while recording).
* `@<letter>`: Execute macro from register `<letter>` (e.g., `@a`).
* `@@`: Repeat the last executed macro.
* `[count]@<letter>`: Execute macro `[count]` times.
* You can view macro content using `:reg <letter>`.
* Macros are stored in registers, so yanking/deleting also affects them if you use the same register.

## Miscellaneous

* `K`: Lookup the keyword under the cursor using the configured `keywordprg` (often `man` or language-specific help).
* `Ctrl+g`: Show current file name, status, and cursor position.
* `ga`: Show ASCII, hex, and octal value of character under cursor.
* `gf`: Go to file name under cursor (open it in current window).
* `Ctrl+a`: Increment number under cursor.
* `Ctrl+x`: Decrement number under cursor.
* `:set paste`: Set paste mode (prevents auto-indent and other formatting issues when pasting from external sources).
* `:set nopaste`: Disable paste mode.
* `Ctrl+z`: Suspend Vim (send to background, use `fg` in shell to resume).
* `:colorscheme <name>`: Change color scheme (e.g., `:colorscheme desert`).
* `:syntax on/off`: Enable/disable syntax highlighting.
* `~/.vimrc` or `~/.config/nvim/init.vim` (for Neovim): Vim configuration file.

---

This cheatsheet covers a wide range of Vim's capabilities. For more in-depth information, use Vim's built-in help system: `:help` or `:help <command>`.
