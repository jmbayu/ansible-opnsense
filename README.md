# OPNsense Ansible Provisioning

Simple way to manage OPNsense via Ansible API.

## Setup

1. **Dependencies:**
   ```bash
   pip install httpx
   ansible-galaxy collection install oxlorg.opnsense
   ```
2. **Firewall:** Enable SSH and create an API key in **System > Access > Users**.
3. **Configure:** Update `hosts.yml` with your firewall IP and API credentials.

## Usage

- **Gather existing config:**
  ```bash
  ansible-playbook -i hosts.yml gather_facts.yml
  ```
- **Apply configuration:**
  ```bash
  ansible-playbook -i hosts.yml provision.yml
  ```

Files are saved in the `input/` folder as YAML.
