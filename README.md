# `nvim-lite`
A neovim config that strives to be as simple as possible, while remaining usable

## Anti Goals
- Tabs
- Splits

Years of using these features have caused me repeated frustrations, such as:
- Having to think about where a tab/window is, or if it's even open
- Wanting to reorganize my buffer layout, moving splits to other tabs, or tabs
to other splits, etc...

`nvim-lite` is an experiment to try to take all this friction out, and still
make the best possible editor experience. I only have two eyes, I don't need
more than one buffer at a time.

## Goals
- Speed (of editor and of use)
- Out of your way (if it's on the screen, it better be *really* important)

## How do I try this

If you want to try this configuration without having to touch your existing one,
a nice trick is to:

1. Clone this repository somewhere on your system
2. `ln -s /path/to/repo $HOME/.config/`

Now if you run `NVIM_APPNAME="nvim-lite" nvim`, it should start with this
config. If you end up liking it, you can even alias that last command.

```
alias nvim-lite="NVIM_APPNAME=nvim-lite nvim"
```

If you don't end up liking it, you just have to delete `$HOME/.config/nvim-lite`
and `$HOME/.local/share/nvim-lite`.

## So how do I use this?

If you're used to the vscode-like neovim interfaces, this might seem like a big
change. This config does everything it can to encourage you to spend less time
on things that don't matter, like cycling through tabs or going down a file
tree. It also tries very hard to make all the most important stuff as accessible
as possible.

1. Use the [jumplist](https://neovim.io/doc/user/motion.html#_8.-jumps).
2. Use [Telescope](https://github.com/nvim-telescope/telescope.nvim). This
   configuration comes with handy [key binds](#key_bindings) for live grep, find
   files, and file browser.

## Key Bindings

*This configuration is still in its early stages, expect changes.*

In general, you can find all the system keybinds in
[keybinds](./lua/config/keybinds.lua). Some of the more important ones are
listed below. In all of these, space is the leader key.

### Movement

- `ctrl` + `o`: Go back a jump
- `ctrl` + `i`: Go forward a jump
- `<leader>t`: Opens [Telescope file browser](https://github.com/nvim-telescope/telescope-file-browser.nvim)
  Inside of the file browser:
  - `k/j`: goes up/down
  - `l`: opens the file/directory
  - `h`: goes back a directory
  - `a`: creates a file in the current directory
- `<leader>f`: Opens the default Telescope file searcher
- `<leader>l`: Opens the default Telescope live grepper.

### Git

This configuration comes with
[`Diffview`](https://github.com/sindrets/diffview.nvim/) and
[`Gitsigns`](https://github.com/lewis6991/gitsigns.nvim).

- `<leader>dd`: Toggle `Diffview`
- `<leader>dh`: Toggle `Diffview` File History
- `<leader>gs`: Stage hunk
- `<leader>gr`: Reset hunk
- `<leader>gS`: Unstage hunk

## Theming

Theming is powered by [`llGaetanll/base16`](https://github.com/llGaetanll/base16.nvim), which exposes the `:Theme` command.

## TODO
- [x] A basic user guide would be nice
- [x] `nvim-autopairs` doesn't work, parentheses, and quotes are not auto completed
- [x] Keybinds to move between windows actually move the windows themselves
- [x] lsp loads all configs upfront, instead of just the ones loaded into the buffer
- [x] `Gitsigns` toggle hunk in keybinds doesn't actually toggle hunks
- [x] Add lsp-specific config file support
- [x] Only enable mouse for left click
- [x] Configure file management keybinds in Telescope file browser 
- [x] Document theming. Base16 is still young, but quite powerful already.
- [x] Telescope file finder opens the file in Diffview if it's open over it
- [x] Put **all** keybinds in keybinds file, and export them to the right places
- [x] Format typescript files
- [x] Telescope files finder prevents us from closing nvim if it's the only item
- [x] Indents don't adapt to the theme's colors
- [x] Indent can be guessed wrong when creating a new file.
- [x] Disable "open in new tab" keybind in Telescope
- [ ] Diffview colors on theme change appear wrong.
      Example: Start on theme `everforest`, switch to `default-dark`. Colors
      appear different with diffs then vs on restart.
- [ ] Telescope file browser / live grep / file finder have keybind disparities
      - [ ] `l` can be used in file browser to open a file but not in file finder or
        live grep
      - [ ] `ctrl` + `i/o` (split open) only work in file browser
- [ ] It should be easier to see if a large project has lsp error (maybe just in
      files that are not open)
- [ ] Seeing the git branch in the nvim line would be nice.
      I'm relunctant on using lualine, mostly for speed reasons.
- [ ] Telescope find files could use something to toggle git ignore in search
      results maybe?
- [ ] lsp does not listen to rustfmt.toml
- [ ] Telescope lsp references should not list the function definition
- [ ] Add commit/pull/push support from inside nvim? Currently using Diffview &
      Gitsigns, can't find a good plugin just for this.
- [ ] Custom colorschemes are great, but some colors need to be consistent
      across themes (i.e. red for errors/diffremove, orange for
      warnings/diffchange, green for diffadd etc..) This is a bigger issue and
      likely needs to be addressed either in
      [`llGaetanll/base16.nvim`](https://github.com/llGaetanll/base16.nvim) or
      [`llGaetanll/prisma.nvim`](https://github.com/llGaetanll/prisma.nvim). In
      the meantime, if you need a theme with "correct enough" colors,
      `default-dark` is your friend.
