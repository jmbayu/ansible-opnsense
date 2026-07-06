# Agent Instructions for OPNsense-Ansible Project

## Overview
This project uses Ansible to provision and manage OPNsense firewalls via the official REST API.

## Core Principles
- **Collection Choice:** Use `oxlorg.opnsense` (formerly `ansibleguy.opnsense`). It is the community standard for OPNsense API management.
- **Connection Mode:** Always use `ansible_connection: local` as the modules run on the control node and communicate with the OPNsense API.
- **Security:** Do not commit raw API keys or secrets. Use placeholders or Ansible Vault.

## Project Structure
- `opnsense-ansible/inventory/`: Contains host definitions and group variables.
- `opnsense-ansible/playbooks/`:
    - `provision.yml`: Uses dynamic loading to apply configuration from the `input/` directory.
    - `gather_facts.yml`: Extracts configuration from a live firewall and saves it to the `input/` directory.
- `opnsense-ansible/input/`: Stores YAML-formatted configuration facts (e.g., `alias.yml`, `rule.yml`).

## Module Specifics
- **Module Defaults:** Use `group/oxlorg.opnsense.all` in `module_defaults` to centralize connection parameters (`firewall`, `api_key`, `api_secret`, `ssl_verify`).
- **Firewall URL:** The `firewall` variable should be the base URL (e.g., `https://192.168.1.1`). Do NOT include the `/api` suffix.
- **Gathering Logic:** When using `oxlorg.opnsense.list`, results are returned in a dictionary key named after the resource (e.g., `item.alias`).

## Validation
- Ensure all YAML files are syntactically valid.
- You can run the following check to verify syntax across the project:
  ```bash
  python3 -c "import yaml, glob; [yaml.safe_load(open(f)) for f in glob.glob('opnsense-ansible/**/*.yml', recursive=True)]"
  ```
