# Agent Instructions

## Principles
- **Keep it Simple:** Use a flat directory structure.
- **API Management:** Use `oxlorg.opnsense` collection with `ansible_connection: local`.
- **No Fact Gathering:** Use `gather_facts: false` to avoid SSH dependencies.

## Structure
- `hosts.yml`: Combined inventory and connection variables.
- `gather_facts.yml`: Extracts config to `input/`.
- `provision.yml`: Plays back config from `input/`.
- `input/`: YAML configuration files.

## Validation
```bash
python3 -c "import yaml, glob; [yaml.safe_load(open(f)) for f in glob.glob('*.yml')]"
```
