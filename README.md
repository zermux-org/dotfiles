# Zermux Dotfiles 🚀  
**Your Android phone → real dev machine. Zero boilerplate. One command. Fully reproducible.**

<img src="https://raw.githubusercontent.com/zermux-org/dotfiles/main/screenshot.png" alt="Tokyo Night Termux with Starship + Neovim" width="100%"/>

```bash
git clone https://github.com/zermux-org/dotfiles.git && cd dotfiles && ./install.sh
```

That’s it. 30 seconds later you have a beautiful, powerful, Git-backed terminal environment.

## What You Get (Instantly)

| Category           | Included Goodies                                                                                           |
|--------------------|------------------------------------------------------------------------------------------------------------|
| **Shell**          | Bash (ble.sh) + Zsh • Starship • Carapace completions • Modern keybindings                                 |
| **Editor**         | Neovim + LazyVim • Tokyo Night transparent • LSPs for Lua, Bash, NuShell, TOML                             |
| **Termux Look**    | Tokyo Night colors • Gradient ASCII MOTD • Custom font • sshd auto-start on boot                           |
| **Termux Power**   | Optimized `termux.properties` • Wake-lock • Extra-keys ready • All configs in `~/.termux/`                 |
| **Management**     | Chezmoi (declarative + encrypted secrets) • OpenSpec change proposals • Idempotent install.sh              |
| **Extras**         | Crush AI config (Gemini + Ollama) • Vivid colors • Clean XDG & PATH                                        |

Everything is version-controlled, secrets stay encrypted (`private_` prefix), and `chezmoi diff` lets you preview every change.

## Essential Chezmoi Commands

```bash
./install.sh               # First-time setup (idempotent, safe to re-run)
chezmoi diff               # Preview what will change (always do this!)
chezmoi apply              # Apply changes
chezmoi update             # git pull + apply latest
```

## Repository Structure

- `home/` → chezmoi source  
  → `dot_` files become hidden (e.g. `dot_bashrc` → `~/.bashrc`)  
  → `private_dot_termux/` → becomes `~/.termux/` (with secret support)
- `openspec/` → formal spec-driven change process (see AGENTS.md)

## Important Rules (Never Fight Chezmoi)

- Edit files inside this repo only → never touch `~/.*` directly (they’ll be overwritten)
- Secrets go in `private_*` files → chezmoi encrypts them with your backend (1Password, pass, Bitwarden…)
- Big changes? Follow the OpenSpec process in `openspec/` — keeps everything safe and reviewable

## Roadmap

| Version | Features                                                                                 | Status     |
|---------|------------------------------------------------------------------------------------------|------------|
| v1.0    | Current: Core Termux + Neovim + Shells + Chezmoi + OpenSpec                              | Released   |
| v1.1    | Smart extra-keys rows • Taskfile.yml runner                                              | Next       |
| v1.2    | Tmux + auto-resurrect • Lazygit + delta                                                  | Planned    |
| v1.3    | Proot-distro manager • Docker-in-Termux toolkit                                          | Planned    |
| v1.4    | Local AI suite (Ollama + Continue.dev)                                                   | Planned    |
| v1.5    | Automated git + restic backups                                                           | Planned    |
| v2.0    | Multi-device sync • Web dashboard                                                        | Dream      |

## Contributing

1. Fork
2. Create an OpenSpec proposal in `openspec/changes/`
3. PR → merge → profit

Star ★ this repo if you believe every Android phone deserves real tools.

**Zermux.org — Because phones can code too.**