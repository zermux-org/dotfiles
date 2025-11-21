# Termux Configuration Management Specification

This specification details the requirements for managing Termux configuration files within the chezmoi dotfiles repository.

## ADDED Requirements

### Requirement: Termux Configuration Source Structure

Termux configuration files MUST be organized within the chezmoi source directory under `home/private_dot_termux/`, mirroring the target `~/.termux/` structure.

#### Scenario: Basic configuration file placement

Given a Termux configuration file `colors.properties`
When it is placed in `home/private_dot_termux/colors.properties`
Then `chezmoi` MUST ensure it is deployed to `~/.termux/colors.properties` on the target system.

### Requirement: Secure Handling of Sensitive Termux Data

Sensitive Termux configuration files MUST be prefixed with `private_` in the chezmoi source directory to leverage chezmoi's secret management capabilities.

#### Scenario: Deployment of a sensitive environment file

Given a sensitive Termux environment file `secrets.env`
When it is placed in `home/private_dot_termux/private_secrets.env`
Then `chezmoi` MUST encrypt/decrypt and deploy it to `~/.termux/secrets.env` on the target system, respecting the configured secret backend.

### Requirement: Idempotent Deployment

Repeated application of Termux configurations via `chezmoi apply` MUST result in the same target state without errors or unintended side effects.

#### Scenario: Re-applying existing configurations

Given Termux configurations have already been deployed to `~/.termux/`
When `chezmoi apply` is executed again
Then the target configuration files MUST remain unchanged unless modifications were made in the chezmoi source, and no errors MUST be reported due to existing files.

### Requirement: Compatibility with `install.sh`

The integration of Termux configurations MUST be compatible with the existing `install.sh` script, allowing for seamless initial setup and updates.

#### Scenario: Initial installation with install.sh

Given a fresh Termux environment
When `install.sh` is executed
Then all Termux configurations, including sensitive files, MUST be correctly deployed to `~/.termux/`.
