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
`Examples` contains more details, for actual snippets take a look at [my Snippets](https://github.com/L3MON4D3/Dotfiles/blob/master/.config/nvim/lua/snips.lua).

Inspired by [vsnip.vim](https://github.com/hrsh7th/vim-vsnip/)
