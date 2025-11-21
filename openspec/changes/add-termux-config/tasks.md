# Tasks: Integrate Termux Configuration into Chezmoi

This document outlines the ordered tasks required to integrate Termux configurations into the chezmoi dotfiles repository.

1.  **Define Termux Configuration Management Spec**
    *   Create `openspec/changes/add-termux-config/specs/termux-config-management/spec.md`.
    *   Draft requirements and scenarios for Termux dotfile structure, deployment, and secure handling of sensitive data using `private_` prefix.
    *   Ensure the spec covers the mapping from `home/private_dot_termux/` to `~/.termux/`.

2.  **Move Existing Termux Configurations**
    *   Identify existing Termux configuration files in `home/private_dot_termux/` (if any, currently untracked).
    *   Move or copy these files into the `home/private_dot_termux/` directory within the chezmoi source.
    *   Ensure sensitive files are renamed with the `private_` prefix as per the design.

3.  **Update Chezmoi Source Directory**
    *   Add a dummy file (e.g., `home/private_dot_termux/config`) to the chezmoi source to establish the directory structure.

4.  **Verify `install.sh` for Termux Deployment**
    *   Review `install.sh` to confirm `chezmoi init --apply` or `chezmoi apply` commands are sufficient for deploying the new Termux configurations.
    *   No explicit changes to `install.sh` are expected unless a specific Termux-related setup step is required that chezmoi doesn't handle natively.

5.  **Validate Changes with `chezmoi diff`**
    *   Run `chezmoi diff` to preview the changes chezmoi would make to the target Termux configuration directory (`~/.termux/`).
    *   Verify that files are correctly staged for deployment and sensitive files are appropriately managed.

6.  **Apply Changes with `chezmoi apply`**
    *   Execute `chezmoi apply` to deploy the Termux configurations to the home directory.
    *   Verify files are in their correct locations and permissions are set as expected.

7.  **Functional Testing (Manual)**
    *   Open Termux and verify that the applied configurations (e.g., `.bashrc` changes) are active and functional.
    *   Confirm that any simulated sensitive files are correctly handled (e.g., decrypted and present in the target location, if applicable).
