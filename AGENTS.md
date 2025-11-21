<!-- OPENSPEC:START -->
# OpenSpec Instructions

These instructions are for AI assistants working in this project.

Always open `@/openspec/AGENTS.md` when the request:
- Mentions planning or proposals (words like proposal, spec, change, plan)
- Introduces new capabilities, breaking changes, architecture shifts, or big performance/security work
- Sounds ambiguous and you need the authoritative spec before coding

Use `@/openspec/AGENTS.md` to learn:
- How to create and apply change proposals
- Spec format and conventions
- Project structure and guidelines

Keep this managed block so 'openspec update' can refresh the instructions.

<!-- OPENSPEC:END -->

# Chezmoi Dotfiles Repository Guide

This repository contains a zero-boilerplate, Git-backed, chezmoi-powered declarative configuration tool that turns your Android phone into a reproducible Terminal Development Environment.

## Core Tools

- `chezmoi`: The primary tool for managing and deploying dotfiles.

## Essential Commands

- **Setup/Apply Changes**:
    ```bash
    ./install.sh
    ```
    This script installs `chezmoi` if it's not found and then runs `chezmoi init --apply --source="${script_dir}"` to apply all dotfiles from this repository.

- **View Pending Changes**:
    ```bash
    chezmoi diff
    ```
    Shows a diff of the changes that `chezmoi` would make to the target state. Always use this before applying changes.

- **Apply Changes**:
    ```bash
    chezmoi apply
    ```
    Applies the dotfiles from the source directory to the destination (usually the home directory).

- **Update and Apply**:
    ```bash
    chezmoi update
    ```
    Pulls the latest changes from the repository and applies them.

## Code Organization and Structure

- **`home/`**: This directory contains the source dotfiles. The structure mirrors the target home directory, with `dot_` prefixes for hidden files/directories (e.g., `home/dot_bashrc` maps to `~/.bashrc`, `home/dot_config/nvim` maps to `~/.config/nvim`).
- **`openspec/`**: Contains specifications and change proposals for how changes should be introduced and managed within this repository. Agents should refer to this directory for guidance on structured changes.

## Naming Conventions and Style Patterns

- Follow existing naming conventions and style within the respective dotfiles (e.g., shell scripts, Neovim Lua configurations). When in doubt, mimic the surrounding code.

## Testing Approach

- The primary "testing" mechanism for dotfiles is `chezmoi diff` to review changes before they are applied to the system.
- For Neovim configurations (`home/dot_config/nvim`), ensure that changes do not introduce syntax errors and integrate correctly by opening Neovim after applying.

## Important Gotchas and Non-obvious Patterns

- **Chezmoi Management**: All modifications to dotfiles should ideally be made through `chezmoi`'s source directory (`home/`). Avoid manual edits to the target files in the home directory, as they will be overwritten by `chezmoi`.
- **OpenSpec Process**: Any significant changes or new features should follow the `openspec` proposal process, as detailed in the `openspec/AGENTS.md` file. Always check for relevant specs before implementing.
- **`install.sh`**: This script is idempotent and safe to run multiple times for initial setup and updates.
