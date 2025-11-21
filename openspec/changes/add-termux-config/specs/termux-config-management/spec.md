# Specification: Termux Configuration Management

## 1. Introduction

This specification details the integration of Termux-specific configuration files into the chezmoi dotfiles repository. The primary objective is to enable consistent, version-controlled deployment and secure management of Termux settings across different Android devices.

## 2. Directory Structure

Termux configuration files shall be organized under `home/private_dot_termux/` within the chezmoi source directory. This structure directly maps to the target `~/.termux/` directory on the Termux environment.

- `home/private_dot_termux/`: Root for all Termux configurations.
- `home/private_dot_termux/config`: A placeholder or general configuration file for Termux.
- `home/private_dot_termux/colors.properties`: Example for Termux terminal color scheme.
- `home/private_dot_termux/font.ttf`: Example for Termux terminal font.
- `home/private_dot_termux/termux.properties`: Main Termux application settings.
- `home/private_dot_termux/boot/start-sshd`: Example boot script for starting SSH daemon.
- `home/private_dot_termux/private_motd.sh`: Example for a Message Of The Day script, prefixed `private_` to denote potential sensitive content or user-specific customization not intended for public sharing.

## 3. Deployment and Synchronization

### 3.1 Initial Setup

The `install.sh` script, which executes `chezmoi init --apply`, will be responsible for the initial deployment of Termux configurations. Chezmoi will automatically create the `~/.termux/` directory and deploy its contents based on the source files in `home/private_dot_termux/`.

### 3.2 Updates

Subsequent synchronization of Termux configurations will be handled by `chezmoi apply` or `chezmoi update`. These commands will apply any changes from the source repository to the target Termux environment, ensuring configurations remain up-to-date.

### 3.3 Idempotency

All chezmoi operations related to Termux configurations must be idempotent. Repeated application of configurations should not lead to errors or unintended side effects.

## 4. Secure Handling of Sensitive Data

Sensitive Termux configurations, such as API keys, tokens, or other user-specific data, shall be managed using chezmoi's `private_` file prefix feature.

### 4.1 `private_` Prefix

Any file or directory prefixed with `private_` within `home/private_dot_termux/` will be treated as a secret by chezmoi. Chezmoi will encrypt these files at rest in the source repository and decrypt them upon deployment to the target `~/.termux/` directory.

Example: `home/private_dot_termux/private_motd.sh` will be deployed as `~/.termux/motd.sh`, with its content decrypted (if encrypted by chezmoi's secret management).

### 4.2 User Responsibility

Users are responsible for configuring chezmoi's secret management (e.g., integration with `pass`, 1Password, LastPass) to properly handle `private_` prefixed files. The repository will provide examples but will not contain plaintext sensitive data.

## 5. Requirements

- R1: Termux configuration files must be version-controlled within the chezmoi repository.
- R2: Deployment of Termux configurations must be automated via `chezmoi init --apply` and `chezmoi apply`.
- R3: The directory `home/private_dot_termux/` must map to `~/.termux/` on the target system.
- R4: Sensitive Termux configurations must be managed securely using chezmoi's `private_` prefix.
- R5: The system must support placeholder files for establishing directory structure without actual content.

## 6. Scenarios

- **Scenario 1: New Termux Installation**
    1. User installs Termux on a new device.
    2. User clones the chezmoi repository.
    3. User runs `install.sh`.
    4. Expected: `~/.termux/` is created, and all configurations from `home/private_dot_termux/` (including decrypted `private_` files) are deployed.

- **Scenario 2: Updating Termux Configurations**
    1. User modifies a Termux configuration file (e.g., `colors.properties`) in the chezmoi source.
    2. User runs `chezmoi apply` or `chezmoi update`.
    3. Expected: The updated `colors.properties` is deployed to `~/.termux/colors.properties`.

- **Scenario 3: Handling Sensitive Data**
    1. User adds a new sensitive script `private_script.sh` to `home/private_dot_termux/`.
    2. User commits and pushes changes.
    3. Expected: `private_script.sh` is encrypted in the repository. Upon deployment, it is decrypted and placed as `~/.termux/script.sh`.
