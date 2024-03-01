# rajayonin's Vim cheatsheet
My personal cheatsheet for Vim/Neovim, with the actions/commands I tend to use.  

Vim is quite useful and powerful, specially for shell-only enviroments (servers, ssh, etc.), and I think every computer engineer/technician should learn at least the basics.  

Don't suffer too much!

## Modes
There are 3 modes on Vim, each mode having its own specific rules:
1. **NORMAL mode:** Keypresses represent [actions](#actions).  
It's the default mode, but you can enter it by pressing `Esc`.
2. **INSERT mode:** Keypresses represent regular characters.  
There are many ways of entering it (see [Insertion](#insertion)).
3. **VISUAL mode:** Here you can select characters using [movement actions](#movement). Unlike the other modes, you perform [visual actions](#visual-actions) instead of regular [actions](#actions).  
Enter it by pressing `v`. You can also exit by pressing `v`.
    1. **VISUAL LINE mode:** Selects whole lines.
        Enter it by pressing `V`. You can also exit by pressing `V`.
    2. **VISUAL BLOCK mode:** Allows to select the same columns across multiple lines.
        Enter it by pressing `Ctrl`+`v`. You can also exit by pressing `Ctrl`+`v`.


## Actions
Actions are the main part of Vim, and allow you to do all sorts of stuff to the text.  
The following actions can only be done in NORMAL mode.  
To cancel any action, press `Esc`.

### Movement

- `h` / `j` / `k` / `l` - **move**  
Move cursor _left_ / _down_ / _up_ / _right_.
- `w` - **word**  
Move cursor to the beginning of the next word.
- `e` - **end**  
Move cursor to the end of the word
- `b` - **beginning**  
Move cursor to the beginning of the previous word.
- `0` - **start of line**  
Move cursor to the beginning of the line.
- `$` - **end of line**  
Move cursor to the end of the line.
- `%` - **parenthesis**  
Move cursor to matching parenthesis.
- `}` / `{` - **block**  
Jump to _next_ / _previous_ block/paragraph
- `gg` / `G` - **goto**    
Move cursor to the _beginning_ / _end_ of the file.
    - `[n]gg` - **goto line**  
    Move cursor to the beginning of line _`n`_.

### Insertion

- `i` / `I` - **insert**  
Enter INSERT mode _at cursor_ / at beginning of line
- `a` / `A` - **append**  
Enter INSERT mode _after_ the cursor / _at the end of the line_.   
Useful in combination with end, e.g. `ea` inserts to the end of the word.
- `o` / `O` - **newline**  
Add a new line _after_ / _before_ the current one, enter INSERT mode on new line.
<!--- `s`, `S` - **supress**  
Delete character under the cursor/current line, enter INSERT mode. -->

### Edition

- `r[char]` - **replace**  
Replace character under cursor with _`char`_.  
- `x` / `X` - **remove**  
Remove character _at_ / _before_ cursor.
- `d[movement]` - **delete** (cut)  
Delete characters in the range of the [movement](#movement) _`movement`_, and copy to clipboard.  
Eg.: `de` deletes until the end of the word.
    - `dd` - **delete line**  
    Delete the current line, copy to clipboard.   
    Moves cursor to the beginning of next line.
    - `D`  
    Deletes until the end of the current line.
- `J` / `gJ` - **join**  
Join line below the current one, _with_ / _without_ one space in between.
- `>>` / `<<` - **indent / de-indent**  
_Indent_ / _de-indent_ current line one shiftwidth.
    - `>%` / `<%` - **indent/de-indent block**  
    _Indent_ / _de-indent_ current paragraph one shiftwidth.
- `==` - **re-indent**  
Remove indentation of the current line.
    - `=%` - **re-indent block**  
    Re-indent current block.
- `gu[movement]` / `gU[movement]` - **upper / lower case**  
Change to _upper_ / _lower_ case in the range of the [movement](#movement) _`movement`_.
- `y[movement]` - **yank** (copy)  
Copy characters in the [movement](#movement) _`movement`_ to clipboard.
    - `yy` - **yank line**  
    Copy the current line to clipboard.
- `p` / `P` - **put** (paste)  
Paste the clipboard _after_ / _before_ cursor.
- `u` - **undo**  
Undo last change. This includes actions and everything done in INSERT mode.
    - `U` - **restore line**  
    Restore changes to the last modified line.
- `Ctrl`+`r` - **redo**  
Redo last undo.
- `.` - **repeat action**  
Repeat last action.

### Search
- `f[char]` / `F[char]` - **find**  
Move to _next_ / _previous_ _`char`_ in line.
    - `;` / `,` - **repeat find**  
    Repeat last _next_ / _previous_ find.
- `/[text]` - **search**  
Search _`text`_.
Remember to press `Enter` afterwards.
    - `n` / `N` - **next / previous match**
      Go to _next_ / _previous_ match.
- `gd` - **goto declaration**
  Move to the declaration of the symbol under the cursor (variable, function, etc.).
- `*` - **goto next**  
  Goes to the next occurence of the word under the cursor.

### Action modifiers
- `[n][action]` - **repeat**  
Repeats _`action`_ _`n`_ times.

### Other
- `Ctrl`+`y` / `Ctrl`+`e` - **scroll**  
Move screen _up_ / _down_ one line (without moving cursor).
- `Ctrl`+`o` / `Ctrl`+`i` - **go backwards / forwards**  
Moves through the movement history to the _previous_ / _next_ place the cursor was.


## Visual actions
VISUAL mode allows to select chunks of text using [movement actions](#movement), and perform certain actions on them, similar to selecting text with a mouse, making it a very useful tool.  
The actions are similar to the regular ones, but without specifying a movement.

- `c` - **change**  
  Removes selection and enters INSERT mode.
- `y` - **yank**  
  Copies the selection.
- `d` - **delete**  
  Deletes the selection.
- `>` / `<` - **indent / de-indent**  
_Indent_ / _de-indent_ selection one shiftwidth.
    - `[n]>`, `[n]<` - **indent / de-indent n**  
      _Indent_ / _de-indent_ selection _`n`_ shiftwidths.
- `=` - **autoindent**  
  Automatically indents selection.
- `I` - **insert**  
  Enters INSERT mode. In VISUAL BLOCK mode, all text inserted is applied to all previously selected lines.
- `J` - **join**  
  Joins lines in the selection.
- `gu` / `gU` - **upper / lower case**  
    Change the selection to _upper_ / _lower_ case.


## Commands
Commands **can only be executed in NORMAL or VISUAL mode**, and are preceded by `:` In VISUAL mode, the command applies only to the selection.  

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
- `:![sh command]` - **shell comand**  
Executes the specified _`sh comand`_ shell command.
- `:s[d][search][d][replace][d]g` - **search and replace**  
Replaces all ocurences of _`search`_ with _`replace`_ within the current line (or selection if VISUAL mode), using the character _`d`_ as a delimeter. This follows [sed](https://www.gnu.org/software/sed/manual/sed.html)'s syntax.
    - Use `%s` to affect the full file.
    - Add `i` at the end for case insensitive.
    - The delimiter is any character to separate the different parts, preferably that is not in _`search`_ or _`replace`_ so that you don't need to escape it. Traditionally, it's `/`. 

Commands can be "forced" by adding `!` at the end.  
Eg.: `:q!` - force quit.


## Macros
Macros are series of inputs that can be recorded and redone, extremely useful for repeatable stuff you have to do in an specific file.

- `q[macro]` - **start macro**  
Start recording a new macro named _`macro`_.
    - `q` - **stop macro**  
    Stop recording the current macro.
- `@[macro]` - **run macro**  
Run _`macro`_.
    - `@@` - **rerun macro**  
    Rerun last macro.


## Clipboard
When yanking or pasting text in Vim, it only works _inside_ of Vim, that is, you can't copy stuff into/from your system's clipboard.  
In order to access your system's clipboard, use `"+` before any yank, delete, or paste.  

Alternatively, you can set your system's clipboard as default by adding `set clipboard=unnamed` to your `.vimrc`[^1] (see [configuration](#configuration)).  

For this to work, remember to install `vim-gtk3`.

[^1]: For Neovim users using Lua config, use `vim.opt.clipboard = 'unnamedplus'`.

## Configuration
Config files are stored in `~/.vimrc`. You can check my personal configuration [here](https://github.com/rajayonin/dotfiles/blob/main/.vimrc).

<!-- TODO: vimrc -->


## More information
- For a more exhaustive cheatsheet please check [Vim Cheat Sheet](https://vim.rtorr.com/).
- For a quite useful interactive Vim tutorial and console please check [Interactive Vim tutorial](https://openvim.com/tutorial.html).
- For an online Vim editor, go to [Vim Online Editor](https://www.vimonlineeditor.com/).
- For a more in-depth reference guide, check out [Vim reference](https://learnbyexample.github.io/vim_reference/) or consult the manual (`man vim`).
- If you also want to see what Vim can do (plugins, etc), watch [CTT's video](https://youtu.be/P88ydZVcm1s).
- May I suggest using [Neovim](https://neovim.io/) instead of Vim? It's _like_ Vim, but with better performance, easier configuration, better plugins, and better overall support.
    - You can also check out [neovim-learning](https://github.com/guluc3m/neovim-learning).
