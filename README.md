Vim-asciiville is a dark & light color scheme designed to use on vim, gvim and neovim. It consists of 16 colors selected procedurally (algorithms). It has support for 8, 16 and 256 colors, and *True Color* (24 bits) on the last versions of vim, gvim, neovim and nvim-qt. It uses the setting `termguicolors` properly (some color schemes don't).

It also includes ten modes of color:
- Dark blue, soft contrast
- Dark blue, hard contrast
- Dark cyan, soft contrast
- Dark cyan, hard contrast
- Night orange, soft contrast
- Night orange, hard contrast
- Night red, soft contrast
- Night red, hard contrast
- Light sepia, soft contrast
- Light sepia, hard contrast

## Installation

#### Manual installation

1. Copy the file `asciiville.vim` to your `~/.vim/colors/` directory (for vim) or `~/.config/nvim/colors/` directory (for neovim).

```bash
cd vim-asciiville
cp asciiville.vim ~/.vim/colors/
```

#### Using a plugin manager (i.e., [vim-plug](https://github.com/junegunn/vim-plug))

1. Paste this in your `.vimrc` file:
```viml
Plug 'gerardbm/vim-asciiville'
```
2. Reload your settings and install it:
```viml
:source $MYVIMRC
:PlugInstall
```

#### Modify your .vimrc

1. Set the colorscheme in your `.vimrc` configuration file:
```viml
syntax enable
colorscheme asciiville
```

## Configuration

#### Color support

If your terminal supports *True color* (1), you can enable it configuring your `~/.vimrc` file with the setting `set termguicolors` (2) **before** the color scheme definition (`colorscheme asciiville`).

---

1. See [https://gist.github.com/XVilka/8346728](https://gist.github.com/XVilka/8346728) for a list of terminals that support *True color*.

2. Sometimes setting `termguicolors` is not enough and one has to set the `t_8f` and `t_8b` options explicitly, also **before** the color scheme definition:

```viml
if has("termguicolors")
	let &t_8f = "\<Esc>[38;2;%lu;%lu;%lum"
	let &t_8b = "\<Esc>[48;2;%lu;%lu;%lum"
	set termguicolors
endif
```

Use it when `$TERM` is not `xterm`, for example, running vim into tmux or using a terminal with different `$TERM`, like st case.

More info, see `:h xterm-true-color`.

#### Color palettes

If your terminal have *True color* support or if you are using a GUI (like gvim or nvim-qt), you have the following commands to switch between the different color palettes:

- (1) `AsciivilleDarkBlueSoft`: sets the dark blue mode, default contrast.
- (2) `AsciivilleDarkBlueHard`: sets the dark blue mode, +5% contrast (background darker).
- (3) `AsciivilleDarkCyanSoft`
- (4) `AsciivilleDarkCyanHard`
- (5) `AsciivilleNightOrangeSoft`
- (6) `AsciivilleNightOrangeHard`
- (7) `AsciivilleNightRedSoft`
- (8) `AsciivilleNightRedHard`
- (9) `AsciivilleLightSoft`
- (10) `AsciivilleLightHard`

Use one of them **after** the color scheme definition in your `~/.vimrc` or `~/.gvimrc`.

Switch them automatically depending on the current time. For example, if you would like to use the AsciivilleLightSoft between 8 am and 8 pm and switch to AsciivilleNightRedHard at night, simply paste this in your `~/.vimrc` or `~/.gvimrc`:

```viml
function! asciivilleSwitcher()
	if (strftime("%H") > 8) && (strftime("%H") < 20)
		AsciivilleLightSoft
	else
		AsciivilleNightRedHard
	endif
endfunction
```

Alternatively, you can cycle them (from 1 to  10) with a shortcut (for example: <kbd>Shift</kbd>+<kbd>F9</kbd>). Paste this in your `~/.gvimrc` or `~/.gvimrc`:

```viml
nnoremap <S-F9> :call CycleModes()<CR>:colorscheme asciiville<CR>
vnoremap <S-F9> :<C-u>call CycleModes()<CR>:colorscheme asciiville<CR>gv
```
#### Emphasis

Some terminals don't handle italics correctly, so in case you need to disable italics set `let g:asciiville_italic=0` in your `~/.vimrc`, **before** the color scheme definition.

Full list of options to disable italic text, bold, underline and undercurl:

```viml
let g:asciiville_italic = 0
let g:asciiville_bold = 0
let g:asciiville_underline = 0
let g:asciiville_undercurl = 0
```

If this options are not defined, default value is 1 for all of them.

#### Example configuration

```viml
if has("termguicolors")
	let &t_8f = "\<Esc>[38;2;%lu;%lu;%lum"
	let &t_8b = "\<Esc>[48;2;%lu;%lu;%lum"
	set termguicolors
endif

syntax enable

let g:asciiville_italic = 0
colorscheme asciiville
AsciivilleNightRedSoft
```
