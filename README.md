# my-secrets

Manage GPG-encrypted secrets in TOML format.

## Installation

```bash
uv pip install -e .
```

## Getting Started

Initialize with interactive setup:

```bash
my-secrets init
```

This will:
- List available GPG keys
- Let you select one or create a new key
- Save config to `~/.config/my-secrets.toml`
- Create encrypted secrets file at `~/.my/secrets.gpg`

## Usage

```bash
my-secrets list                    # List all categories and keys
my-secrets list -c                 # List only category names
my-secrets list work               # List keys in [work] section
my-secrets get work GITHUB_TOKEN   # Get secret value
my-secrets set work API_KEY        # Prompt for value securely
my-secrets set work API_KEY "val"  # Set value directly
my-secrets delete work OLD_KEY     # Delete with confirmation
my-secrets delete -f work OLD_KEY  # Delete without confirmation
my-secrets search TOKEN            # Regex search across all secrets
my-secrets export database         # Output: export KEY='value'
my-secrets export --all            # Export full TOML (for backup)
my-secrets import backup.toml      # Import from TOML file
```

## Backup & Restore

```bash
# Backup
my-secrets export --all > backup.toml

# Restore
my-secrets import backup.toml
```

## Secrets Format

TOML with sections for categories, ENV-style naming:

```toml
[work]
GITHUB_TOKEN = "ghp_xxxx"
AWS_SECRET_KEY = "xxxx"

[database]
POSTGRES_PASSWORD = "xxxx"
REDIS_URL = "redis://localhost"
```

## Configuration

Config file: `~/.config/my-secrets.toml`

```toml
gpg_recipient = "your@email.com"
secrets_file = "/Users/you/.my/secrets.gpg"
```

## Requirements

- Python 3.12+
- GPG
