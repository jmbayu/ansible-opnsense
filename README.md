# Provisioning OPNsense via Ansible

The most effective way to provision OPNsense via Ansible is by using the **`oxlorg.opnsense`** collection (formerly `ansibleguy.opnsense`). It is widely considered the community standard for managing OPNsense via its REST API.

## Recommended Collection

- **Collection:** `oxlorg.opnsense`
- **Installation:**
  ```bash
  ansible-galaxy collection install oxlorg.opnsense
  ```
- **Why:** It provides a comprehensive set of modules for managing firewall rules, aliases, services, VPNs (WireGuard, IPsec), and more, using the official OPNsense API.

## Prerequisites

1.  **Python Dependencies:** The collection requires the `httpx` module on the control machine.
    ```bash
    pip install httpx
    ```
2.  **API Access:** You must enable the API on OPNsense and create an API key/secret pair.
3.  **SSH Access (Optional):** While most modules use the API, SSH is useful for initial bootstrapping or running raw commands.

## Bootstrapping Process

1.  **Enable SSH:**
    - Go to **System > Settings > Administration**.
    - Check **Enable Secure Shell**.
    - Add your SSH public key to the admin user under **System > Access > Users**.
2.  **Create an API User:**
    - Go to **System > Access > Users**.
    - Create a new user (e.g., `ansible-api`) and assign it the necessary privileges (or the `admin` group).
3.  **Generate API Key:**
    - Edit the newly created user and click the **+** button next to **API keys**.
    - A `.key` file will be downloaded containing the `key` and `secret`.

## Project Structure

This repository provides a sample structure in the `opnsense-ansible/` directory:

- `requirements.yml`: Specifies the collection dependency.
- `inventory/hosts.yml`: Defines your firewall hosts.
- `inventory/group_vars/opnsense.yml`: Contains connection variables.
- `playbooks/provision.yml`: A sample playbook for creating aliases and firewall rules.
- `playbooks/gather_facts.yml`: A playbook to extract existing configuration from a firewall.
- `input/`: Directory where gathered configuration files are saved.

## Usage

1.  **Install dependencies:**
    ```bash
    ansible-galaxy collection install -r opnsense-ansible/requirements.yml
    ```
2.  **Configure credentials:**
    Edit `opnsense-ansible/inventory/group_vars/opnsense.yml` with your API key and secret.
3.  **Run the playbook:**
    ```bash
    ansible-playbook -i opnsense-ansible/inventory/hosts.yml opnsense-ansible/playbooks/provision.yml
    ```

## Fact Gathering (Reverse Engineering IaC)

If you have an existing OPNsense installation and want to start managing it via Ansible, you can use the `gather_facts.yml` playbook to extract your current configuration into YAML files.

1.  **Run the gather facts playbook:**
    ```bash
    ansible-playbook -i opnsense-ansible/inventory/hosts.yml opnsense-ansible/playbooks/gather_facts.yml
    ```
2.  **Review the output:**
    Check the `opnsense-ansible/input/` directory for YAML files (e.g., `alias.yml`, `rule.yml`). You can find a comprehensive list of supported resource targets in `opnsense-ansible/playbooks/gather_facts.yml`.
3.  **Version Control:**
    You can now commit these files to Git to track your infrastructure changes over time.
