# Linux Text Editing Notes: vi/vim Basics

It's almost impossible to use Linux for any period of time without needing a text editor, since most Linux configuration files are plain-text files you'll need to edit manually at some point.

If you're using a GNOME desktop, you can run `gedit` (type `gedit` into the Search box and press Enter, or select **Applications → Accessories → gedit**), which is fairly intuitive for editing text.

## Adding Text

To get into input mode, type any of the following letters. When you're finished inputting text, press **Esc** (sometimes twice) to return to command mode.

| Command | Description |
|---|---|
| `a` | Add — input text starting to the right of the cursor |
| `A` | Add at end — input text starting at the end of the current line |
| `i` | Insert — input text starting to the left of the cursor |
| `I` | Insert at beginning — input text starting at the beginning of the current line |
| `o` | Open below — opens a line below the current line and enters insert mode |
| `O` | Open above — opens a line above the current line and enters insert mode |

> **Tip:** When in insert mode, `-- INSERT --` appears at the bottom of the screen.

> **Tip:** Remember the Esc key! It always returns you to command mode. Sometimes you must press it twice — for example, after typing `:` to enter ex mode.

## Moving Around in the Text

| Command | Description |
|---|---|
| Arrow keys | Move up, down, left, right one character at a time |
| `h` / `l` / `j` / `k` | Left / Right / Down / Up |
| `w` | Beginning of next word (delimited by spaces, tabs, or punctuation) |
| `W` | Beginning of next word (delimited by spaces or tabs) |
| `b` | Beginning of previous word (delimited by spaces, tabs, or punctuation) |
| `B` | Beginning of previous word (delimited by spaces or tabs) |
| `0` | Beginning of the current line |
| `$` | End of the current line |
| `H` | Upper-left corner of the screen (first line) |
| `M` | First character of the middle line on screen |
| `L` | Lower-left corner of the screen (last line) |

## Deleting, Copying, and Changing Text

| Command | Description |
|---|---|
| `x` | Delete character under cursor |
| `X` | Delete character before cursor |
| `d<motion>` | Delete text |
| `c<motion>` | Change text |
| `y<motion>` | Yank (copy) text |

**Examples:**

| Command | Description |
|---|---|
| `dw` | Delete a word after the cursor |
| `db` | Delete a word before the cursor |
| `dd` | Delete the entire current line |
| `c$` | Change from cursor to end of line, enter input mode |
| `c0` | Change from cursor to beginning of line, enter input mode |
| `cl` | Erase current letter, enter input mode |
| `cc` | Erase current line, enter input mode |
| `yy` | Copy current line into buffer |
| `y)` | Copy current sentence into buffer |
| `y}` | Copy current paragraph into buffer |

### With Numeric Modifiers

| Command | Description |
|---|---|
| `3dd` | Delete 3 lines starting at the current line |
| `3dw` | Delete the next 3 words |
| `5cl` | Change the next 5 letters |
| `12j` | Move down 12 lines |
| `5cw` | Erase the next 5 words, enter input mode |
| `4y)` | Copy the next 4 sentences |

## Pasting (Putting) Text

| Command | Description |
|---|---|
| `P` | Put copied text to the left of cursor (or above the line, for line-based copies) |
| `p` | Put copied text to the right of cursor (or below the line, for line-based copies) |

## Repeating Commands

After deleting, changing, or pasting text, repeat the action with `.` (period). For example: `cw` to change a word, type the replacement, then find the next occurrence with `n` and press `.` to repeat the change.

## Exiting vi

| Command | Description |
|---|---|
| `ZZ` | Save changes and exit |
| `:w` | Save the file, keep editing |
| `:wq` | Same as `ZZ` |
| `:q` | Quit (only if no unsaved changes) |
| `:q!` | Quit without saving changes |

> **Tip:** If you've really messed up the file, `:q!` is the best way to abandon changes. If you already saved with `:w`, you can still press `u` repeatedly to undo, then save again.

## Helpful Tips for Beginners

- **Esc** — Always returns you to command mode. `Esc` followed by `ZZ` exits and saves.
- **u** — Undo the previous change; keep pressing to undo further back.
- **Ctrl+R** — Redo (undoes your undo).
- **Caps Lock** — Be careful; capitalized commands behave completely differently, with no warning.
- **`:!command`** — Run a shell command from within vi. Example: `:!date`, `:!pwd`, `:!jobs`. Press Enter to return to editing. You can even launch a shell with `:!bash` and `exit` to return to vi (save first!).
- **Ctrl+g** — Shows the filename, current line, total lines, percentage through the file, and cursor column.

## Skipping Around in the File

| Command | Description |
|---|---|
| `Ctrl+f` | Page forward one page |
| `Ctrl+b` | Page back one page |
| `Ctrl+d` | Page forward half a page |
| `Ctrl+u` | Page back half a page |
| `G` | Go to the last line of the file |
| `1G` | Go to the first line of the file |
| `35G` | Go to a specific line number (e.g., 35) |

## Searching for Text

| Command | Description |
|---|---|
| `/hello` | Search forward for "hello" |
| `?goodbye` | Search backward for "goodbye" |
| `/The.*foot` | Search forward for a line containing "The" followed later by "foot" |
| `?[pP]rint` | Search backward for "print" or "Print" |

After a search, press `n` to repeat in the same direction, or `N` for the opposite direction.

## Using ex Mode

Typing `:` moves the cursor to the bottom of the screen and puts you in ex mode, which lets you find and change text across lines.

| Command | Description |
|---|---|
| `:g/Local` | Print every line containing "Local" |
| `:s/Local/Remote` | Replace the first occurrence of "Local" with "Remote" on the current line |
| `:g/Local/s//Remote` | Replace the first occurrence of "Local" with "Remote" on every line |
| `:g/Local/s//Remote/g` | Replace every occurrence of "Local" with "Remote" in the entire file |
| `:g/Local/s//Remote/gp` | Same as above, and print each changed line |

## Learning More

Try running `vimtutor` for an interactive tutorial covering common vim commands and features. You may need to install the `vim-enhanced` package first.



























