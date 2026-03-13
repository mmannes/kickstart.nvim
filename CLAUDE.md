# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a Neovim configuration based on kickstart.nvim. It uses **lazy.nvim** for plugin management. The config lives at `~/.config/nvim`.

## Architecture

- **`init.lua`** — Main configuration file containing editor options, keybindings, and the full lazy.nvim plugin spec (single-file approach from kickstart.nvim)
- **`lua/kickstart/plugins/`** — Optional kickstart-provided plugin configs (autopairs, debug, gitsigns, indent_line, lint, neo-tree). Enable them by uncommenting the corresponding `require` line in init.lua
- **`lua/custom/plugins/`** — User custom plugins. All `.lua` files here are auto-loaded by lazy.nvim. Currently contains Minuet AI completion config
- **`lazy-lock.json`** — Plugin version lockfile managed by lazy.nvim

## Key Conventions

- Leader key is `<Space>`
- netrw is disabled in favor of nvim-tree (`<leader>v` to toggle)
- Tab settings: tabstop=4, softtabstop=4, shiftwidth=4
- Colorscheme: tokyonight-night (with nightfox also installed)

## Plugin Management

Plugins are installed/updated via lazy.nvim. Run `:Lazy` inside Neovim to manage plugins. No external build commands needed — everything bootstraps on first launch.

## External Dependencies

- Ollama server at `192.168.1.192:11434` is used by both Minuet (AI completion, qwen2.5-coder:7b) and CodeCompanion
- CodeCompanion also has a Gemini adapter configured
- LSP servers are managed by Mason (`:Mason` to install/manage). Configured: clangd, pyright, rust_analyzer, intelephense (PHP), lua_ls
- Formatter: stylua (for Lua, via conform.nvim)
- Linter: markdownlint (via nvim-lint)

## Adding New Plugins

Add new plugin specs to `lua/custom/plugins/` as separate `.lua` files that return a lazy.nvim plugin table. This avoids merge conflicts with upstream kickstart changes in `init.lua`.
