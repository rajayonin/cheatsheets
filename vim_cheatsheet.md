# rajayonin's Vim cheatsheet
My personal cheatsheet for Vim, with the actions/commands I currently (and, in the near future, want to) use.  
For a more exhaustive cheatsheet please check [Vim Cheat Sheet](https://vim.rtorr.com/).  
For a quite useful interactive Vim tutorial and console please check [Interactive Vim tutorial](https://openvim.com/tutorial.html).

Vim is quite useful and powerfull, specially for shell-only enviroments, and I think every computer engineer/technician should learn it.  

Don't suffer too much!

# Modes
There are 3 modes on Vim, each mode having its own specific actions:
1. **NORMAL mode:** Keypresses represent actions.  
It's the default mode, but you can enter it by pressing `Esc`.
2. **INSERT mode:** Keypresses represent regular characters.  
There are many ways of entering it (see [Insertion](#insertion)).
3. **VISUAL mode:** Here you can select characters like you would in a regular text editor.  
As I personally don't use it, it's not detailed in this cheatsheet.  
Enter it by pressing `v`.


# Actions
Actions are the main part of Vim, and allow you to do all sorts of stuff to the text.  
The following actions can only be done in NORMAL mode.  
To cancel any action, press `Esc`.

## Movement
- `h`, `j`, `k`, `l` - **move**  
Move cursor left, down, up, or right.
- `w` - **word**  
Move cursor to the beggining of the next word.
- `e` - **end**  
Move cursor to the end of the word
- `b` - **beggining**  
Move cursor to the beggining of the previous word.
- `0` - **start of line**  
Move cursor to the beggining of the line.
- `$` - **end of line**  
Move cursor to the end of the line.
- `%` - **parenthesis**  
Move cursor to matching parenthesis.
- `}`, `{` - **block**  
Jump to next/previous block/paragraph
- `gg`, `G` - **goto**    
Move cursor to the beggining/end of the file.
    - `[n]gg` - **goto line**  
    Move cursor to the beggining of line _n_.

## Insertion

- `i`, `I` - **insert**  
Enter INSERT mode at cursor/at beggining of line
- `a`, `A` - **append**  
Enter INSERT mode after the cursor/end of the line.   
Useful in combination with end: `ea` - insert to the end of the word.
- `o`, `O` - **newline**  
Add a new line after/before the current one, enter INSERT mode on new line.
- `s`, `S` - **supress**  
Delete character under the cursor/current line, enter INSERT mode.

## Edition

- `r[char]` - **replace**  
Replace character under cursor with _char_.  
- `x`, `X` - **remove**  
Remove character at/before cursor.
- `d[movement]` - **delete** (cut)  
Delete characters in the range of _movement_, and copy to clipboard.  
Eg.: `de` deletes until the end of the word.
    - `dd` - **delete line**  
    Delete the current line, copy to clipboard.   
    Moves cursor to the beggining of next line.
    - `D`  
    Deletes until the end of the current line.
- `J`, `gJ` - **join**  
Join line below the current one, with/without one space in between.
- `>>`, `<<` - **indent/de-indent**  
Indent/de-indent current line one shiftwidth.
    - `>%`, `<%` - **indent/de-indent block**  
    Indent/de-indent current paragraph one shiftwidth.
- `==` - **re-indent**  
Remove indentation of the current line.
    - `=%` - **re-indent block**  
    Re-indent current block.
- `gu[movement]`, `gU[movement]` - **upper/lower case**  
Change to upper/lower case in the range of _movement_.
- `y[movement]` - **yank** (copy)  
Copy characters in _movement_ to clipboard.
    - `yy` - **yank line**  
    Copy the current line to clipboard.
- `p`, `P` - **put** (paste)  
Paste the clipboard after/before cursor.
- `u` - **undo**  
Undo last change.  
This includes actions and everything done in INSERT mode.
    - `U` - **restore line**  
    Restore changes to the last modified line.
- `Ctrl`+`r` - **redo**  
Redo last undo.
- `.` - **repeat action**  
Repeat last action.

## Search
- `f[char]`, `F[char]` - **find**  
Move to next/previous _char_ in line.
    - `;`, `,` - **repeat find**  
    Repeat last next/previous find.
- `/[text]` - **search**  
Search _text_.
Remember to press `Enter` afterwards.
    - n, N - **match**  
    Go to next/previous match.

## Action modifiers
- `[n][action]` - **repeat**  
Repeats _action_ _n_ times.

## Other
- `Ctrl`+`y`, `Ctrl`+`e` - **scroll**  
Move screen up/down one line (without moving cursor).


# Commands

Commands can only be executed in NORMAL mode, and are preceded by `:`.  
To execute a command, press `Enter`.  
To cancel any command, press `Esc`.

- `:w` - **write**  
Save current file.
    - `:w [filename]` - **write as**  
    Save current file as _filename_.
- `:q` - **quit**  
Quit Vim.
- `:x` - **save & quit**  
Save current file and quit Vim.

Commands can be "forced" by adding `!` at the end.  
Eg.: `:q!` - **force quit**.


# Macros

Macros are series of inputs that can be recorded and redone.
- `q[macro]` - **start macro**  
Start recording a new macro named _macro_.
    - `q` - **stop macro**  
    Stop recording the current macro.
- `@[macro]` - **run macro**  
Run _macro_.
    - `@@` - **rerun macro**  
    Rerun last macro.


# rajayonin-specific
These are some extra actions/commands I use.  
To use them, they must be included in the .vimrc config file.  
To check my config file, click [here](.vimrc).

- `Alt`+`j`, `Alt`+`k` - **move line up/down**  
Moves current line up/down.
