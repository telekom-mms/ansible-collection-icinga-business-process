# Icinga Business Process Collection for Ansible

This collection contains an Ansible role which does generate configuration for the Icinga business process extension.

## Installation

```bash
ansible-galaxy collection install telekom_mms.icinga_business_process
```

Alternatively put the collection into a requirements.yml-file:

```yaml
---
collections:
- telekom_mms.icinga_business_process
```

## Example using the role

Please see the [README](roles/ansible_icinga_business_process/README.md) of the role.


## Known Issues

If you get this type of error it probably means that a node or service was specified which does not exist in your Icinga configuration:
```bash
"Status code was 200 and not [302]: OK (unknown bytes)"
```

There are some cases where you need to set the variable `icinga_business_process_force_basic_auth` to `true`, otherwise you will get the following error from every play where the Ansible uri module is used:

```bash
AbstractDigestAuthHandler does not support the following scheme: ''Negotiate''
```
## License

GPLv3

## Author Information

* Christoph Sieber
* Daniel Uhlmann
