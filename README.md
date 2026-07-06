# OPNsense GitOps with Ansible

A comprehensive framework for complete OPNsense server provisioning via the REST API. This setup allows you to manage your entire firewall configuration as code.

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

Files are saved in the `input/` folder as YAML. The `gather_facts.yml` playbook is pre-configured with 60+ resource targets to ensure full server coverage.
