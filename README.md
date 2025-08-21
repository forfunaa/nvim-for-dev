# nvim-for-dev — Minimal Neovim Config for Productive Developers
[![Latest Release](https://img.shields.io/github/v/release/forfunaa/nvim-for-dev?label=Releases&color=2b9348)](https://github.com/forfunaa/nvim-for-dev/releases)  
https://github.com/forfunaa/nvim-for-dev/releases

A compact Neovim setup for software engineers who want a clean, fast editor with sane defaults and first-class language support. This repo focuses on minimalism, performance, and common workflows for web, backend, and systems development.

Badges
- Version: [![Latest Release](https://img.shields.io/github/v/release/forfunaa/nvim-for-dev?label=Release)](https://github.com/forfunaa/nvim-for-dev/releases)
- Platform: Linux · macOS · WSL
- Languages: Lua, Vimscript
- Topics: copilot, copilot-chat, css, dev, golang, html, javascript, json, markdown, neovim, nvchad, nvim, python, rustlang, tailwindcss, toml, typescript, yaml, ziglang

Preview
![Neovim screenshot](https://neovim.io/images/logos/neovim-logo-300x300.png)

Why this config
- Keep the editor small and fast.
- Provide LSP, completion, and linting for common languages.
- Ship a curated plugin set with clear defaults.
- Use Lua for core config and allow layer-style customization.
- Work with existing NVChad or other modular setups but remain standalone.

What this repo includes
- A minimal init.lua and modular lua/* config.
- Core plugin list and lazy loader.
- Prebuilt LSP and DAP setups for Go, Python, Rust, TypeScript, Zig.
- Keymap guide focused on motion, code navigation, and quick refactor.
- Themed status / tabline and a small set of icons.

Supported languages and tooling
- Go (gopls, goimports, delve)
- Python (pyright, black, isort)
- Rust (rust-analyzer, cargo)
- TypeScript / JavaScript (tsserver, eslint, prettier)
- HTML / CSS / TailwindCSS
- Zig (zls)
- Markdown, JSON, TOML, YAML

Requirements
- Neovim 0.9+ (Lua API and virtual text)
- Git
- A POSIX shell for install scripts
- Language servers installed via your package manager or Mason (recommended)
- Optional: ripgrep, fd, lazygit, tmux

Quick install (recommended)
This repo ships releases with compressed archives that include an install helper. Visit the Releases page below and download the latest tarball. Extract it and run the install script.

1. Visit the releases page and download the archive:
   https://github.com/forfunaa/nvim-for-dev/releases

2. Example local install steps after downloading the archive (replace file name with the downloaded release):
   - tar -xzf nvim-for-dev-vX.Y.Z.tar.gz
   - cd nvim-for-dev
   - ./install.sh

The release page contains the archive and an install helper. Download the release file and execute the provided install.sh. The script copies files to ~/.config/nvim, installs the plugin manager, and bootstraps Mason for language servers. You can inspect the install.sh before running it.

If you prefer manual install
- Clone into your config directory:
  - git clone https://github.com/forfunaa/nvim-for-dev.git ~/.config/nvim
- Start Neovim and let the plugin manager install plugins:
  - nvim +Lazy! +qa

Files and layout
- init.lua — entrypoint
- lua/
  - core/ — bootstrap, options, autocommands
  - plugins/ — plugin specs, lazy loader
  - lsp/ — LSP server configs and handlers
  - ui/ — colorscheme, statusline, icons
  - mappings.lua — keymaps and remaps
- scripts/install.sh — release install helper
- README.md — this file

Plugins and tools (high level)
- Plugin manager: lazy.nvim
- Completion: nvim-cmp with snippets
- LSP: built-in lspconfig + mason.nvim for server management
- Treesitter for syntax and textobjects
- Telescope for fuzzy search
- Git signs and diff view
- DAP config for debugging
- Copilot and Copilot Chat integrations for code suggestions
The config enables sensible defaults and only loads heavy plugins on demand.

Language server notes
This config uses mason.nvim and lspconfig to manage servers. It enables common server settings:
- on_attach with keymaps for go-to, hover, rename, code actions
- capabilities for completion and snippets
- format-on-save for supported servers (configurable)

Examples
- Go:
  - gopls for analysis
  - goimports for formatting
  - Delve with DAP for debugging
- Python:
  - pyright for type and symbol support
  - black/isort through null-ls for formatting and imports
- Rust:
  - rust-analyzer with inlay hints and cargo integration

Keybindings (high level)
- <leader>f — find files (Telescope)
- <leader>g — git operations (lazygit / git signs)
- <leader>r — rename symbol (LSP)
- gd — go to definition
- gr — find references
- K — hover docs
- <leader>t — run tests (project-specific commands)
- <leader>c — open Copilot Chat panel

Customization
The config uses a small set of user-editable modules. To add or override:
- lua/user/init.lua — user overrides for options and keymaps
- lua/user/plugins.lua — add or disable plugin specs
- lua/user/lsp.lua — add server configs
- colorscheme — set NVIM_COLOR_SCHEME env var or set in lua/user/ui.lua

Performance tips
- Use lazy-loading for large plugins.
- Disable unused LSP servers in lua/user/lsp.lua.
- Set up ripgrep and fd for fast file search.
- Keep treesitter parsers for the languages you use.

Copilot and Copilot Chat
This config integrates GitHub Copilot and Copilot Chat as optional plugins. They stay disabled by default. To enable:
- Add copilot plugin entry in lua/user/plugins.lua with opts enabled
- Configure a Copilot keymap, for example <leader>p to accept suggestions
- Use Copilot Chat as a docked panel for conversational code help

Themes and UI
- Built-in theme based on dark palette with high contrast.
- Statusline shows mode, git branch, LSP diagnostics, and file position.
- Tabline shows open buffers with icons.
- Use an icon font like Nerd Fonts for best experience.

Diagnostics and formatting
- Diagnostics appear as virtual text and in the location list.
- null-ls provides formatters and linters when not available in a server.
- Format on save uses server or null-ls if configured.

Debugging
- DAP configs include adapters for Delve (Go), debugpy (Python), and lldb (Rust).
- Use <leader>d to open debug UI and control sessions.

Examples: VS Code keymap transplant
If you migrate from VS Code, use these mappings:
- <leader>p — Command Palette (Telescope command picker)
- <leader>b — Toggle sidebar (Telescope buffers)
- <leader>f — Format document (LSP formatting)
Adjust these in lua/user/mappings.lua.

Advanced: extend the config
- Write a plugin spec with dependencies and lazy keys.
- Add project-level settings in .nvim.lua in the project root.
- Use pattern-based autocommands for per-language tweaks.

Contributing
- Open an issue for bugs or feature requests.
- Create a branch per change and submit a PR.
- Follow the code style: Lua for logic, small modules, and clear names.
- Keep the core minimal; prefer optional user modules for features.

Security and audit
- Review install.sh in the release archive before executing it.
- The release contains an install script that writes to ~/.config/nvim. The script also bootstraps the plugin manager and installs Mason for language servers. Download the release archive from the Releases page, inspect the script, and run it.

Releases and download
- Get the packaged config and install helper from the Releases page:
  https://github.com/forfunaa/nvim-for-dev/releases
- Download the latest release archive, extract it, and run the included install.sh.
- The install.sh sets up ~/.config/nvim and bootstraps plugins and Mason.

FAQ
Q: Will this overwrite my config?
A: The installer writes to ~/.config/nvim by default. The install script prompts before overwrite. Inspect the script and adjust the target path if you want a custom location.

Q: How do I add a plugin?
A: Add a plugin spec to lua/user/plugins.lua. Use the same format as the existing specs and restart Neovim to let lazy.nvim install it.

Q: How do I change the leader key?
A: Set vim.g.mapleader at the top of lua/user/init.lua and restart Neovim.

Q: Where can I find the LSP logs?
A: Use :LspLog or check the log path printed by the LSP client. Mason installs servers in a known path; refer to Mason docs for details.

Maintenance and roadmap
- Keep core minimal while adding small UX improvements.
- Add first-class support for Zig and other fast-growing languages.
- Improve Copilot Chat integration and keymaps.
- Expand DAP support and test cases for multi-language projects.

Credits and inspired by
- Neovim community
- NVChad for modular ideas
- lazy.nvim and Mason ecosystem
- Treesitter project contributors

License
- MIT License. See the LICENSE file for details.

Contact
- Open issues or PRs on the GitHub repository.

Releases
[![Release Page](https://img.shields.io/badge/Releases-Open%20on%20GitHub-blue?logo=github)](https://github.com/forfunaa/nvim-for-dev/releases)  
Download the release archive from the page, extract it, and run its install.sh to bootstrap the config and dependencies.