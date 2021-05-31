# LuaSnip
Snippet Engine for Neovim written in Lua.
![Javadoc](./Examples/javadoc.gif)

# Features
- Tabstops
- Text-Transformations using Lua functions
- Conditional Expansion
- Defining nested Snippets
- Filetype-specific Snippets
- Choices
- Dynamic Snippet creation
- Regex-Trigger
- Fast, small, simple
- Parse LSP-Style Snippets (Does not, however, support Regex-Transformations)
- Expand LSP-Snippets with [nvim-compe](https://github.com/hrsh7th/nvim-compe)
- Snippet history (jump back into older snippets)

# Drawbacks
- Snippets that make use of the entire functionality of this plugin have to be defined in Lua.

# Requirements
Neovim >= 0.5 (extmarks)

# Setup
- Install using eg. [vim-plug](https://github.com/junegunn/vim-plug)
- Add mappings  
  - Insert key if jumping/expanding/switching choices is not possible:
  ```vim
  imap <silent><expr> <Tab> luasnip#expand_or_jumpable() ? '<Plug>luasnip-expand-or-jump' : '<Tab>'
  imap <silent><expr> <C-E> luasnip#choice_active() ? '<Plug>luasnip-next-choice' : '<C-E>'
  ```
  - Only try expanding the Snippet/jumping:
  ```vim
  imap <silent><expr> <C-l> <cmd>lua require'luasnip'.expand_or_jump()<Cr>
  inoremap <silent> <S-Tab> <cmd>lua require'luasnip'.jump(-1)<Cr>
  ```
  - Mappings for Jumping in Select:
  ```vim
  snoremap <silent> <Tab> <cmd>lua ls.jump(1)<Cr>
  snoremap <silent> <S-Tab> <cmd>lua ls.jump(-1)<Cr>
  ```
- Add Snippets: Snippets have to be added to the `require'luasnip'.snippets`-table.
`Examples` contains more details, for actual snippets take a look at [examples](https://github.com/L3MON4D3/LuaSnip/blob/master/Examples/snippets.lua) or [my Snippets](https://github.com/L3MON4D3/Dotfiles/blob/master/.config/nvim/lua/snips.lua).

For Supertab-like functionality with compe, check out [#1](https://github.com/L3MON4D3/Luasnip/issues/1).

# Config
- `history`: If true, Snippets that were exited can still be jumped back into. As Snippets are not removed when their text is deleted, they have to be removed manually via `LuasnipUnlinkCurrent`.
- `updateevents`: Choose which events trigger an update of the active nodes dependents. Default is just `'InsertLeave'`, `'InsertLeave,TextChanged,TextChangedI'` would update on every change.

Inspired by [vsnip.vim](https://github.com/hrsh7th/vim-vsnip/)
