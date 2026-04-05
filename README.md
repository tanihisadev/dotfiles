# dotfiles

My personal dotfiles for Linux, managed with [GNU Stow](https://www.gnu.org/software/stow/).

## Prerequisites

- **GNU Stow** — install via your package manager:
  ```bash
  # Arch
  sudo pacman -S stow

  # Debian/Ubuntu
  sudo apt install stow

  # Fedora
  sudo dnf install stow
  ```

## Installation

1. **Clone the repo** into your home directory:
   ```bash
   git clone https://github.com/tanihisadev/dotfiles.git ~/dotfiles
   ```

2. **Stow everything** to symlink all configs into `$HOME`:
   ```bash
   cd ~/dotfiles
   stow --target="$HOME" .
   ```

3. **Reload your shell:**
   ```bash
   exec zsh
   ```

## How it works

The repo root mirrors `$HOME` directly — files sit at the same relative paths they'd have if they lived in `~`. GNU Stow symlinks them into place:

```
~/dotfiles/.zshrc        →  ~/.zshrc
~/dotfiles/.config/kitty →  ~/.config/kitty
```

## Updating

```bash
git pull
```

Stow symlinks are permanent, so pulled changes are live immediately.

## Removing symlinks

To remove all symlinks without deleting the source files:
```bash
stow -D --target="$HOME" .
```

## Adding new configs

1. Place the file at the same path it would have under `$HOME`:
   ```
   dotfiles/
   ├── .zshrc
   └── .config/
       └── kitty/
           └── kitty.conf   ← new file goes here, not in a package subdir
   ```
2. Re-stow (safe to run again, only adds new links):
   ```bash
   stow --target="$HOME" .
   ```
