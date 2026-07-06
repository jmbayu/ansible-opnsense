# Agent Instructions

## Principles
- **GitOps First:** Aim for 100% server coverage. All configurations should be derived from the `input/` YAML files.
- **Keep it Simple:** Use a flat directory structure for easy visibility.
- **API Management:** Use `oxlorg.opnsense` collection with `ansible_connection: local`.
- **No Fact Gathering:** Use `gather_facts: false` to avoid SSH/Python dependencies on the firewall.

## Structure
- `hosts.yml`: Combined inventory and connection variables.
- `gather_facts.yml`: Extracts config to `input/`.
- `provision.yml`: Plays back config from `input/`.
- `input/`: YAML configuration files.

## Validation
```bash
python3 -c "import yaml, glob; [yaml.safe_load(open(f)) for f in glob.glob('*.yml')]"
```
