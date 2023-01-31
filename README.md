# Role Name

**updater**, is updating and upgrading the packages.

[![Ansible Lint](https://github.com/MVladislav/ansible-updater/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/MVladislav/ansible-updater/actions/workflows/ansible-lint.yml)
[![Ansible Molecule Test](https://github.com/MVladislav/ansible-updater/actions/workflows/ci.yml/badge.svg)](https://github.com/MVladislav/ansible-updater/actions/workflows/ci.yml)

- Check out for more info how to use **apt**
  - <https://docs.ansible.com/ansible/latest/modules/apt_module.html>

## Requirements

_Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required._

## Role Variables

```yml
updater_time_timezone: Europe/Berlin
updater_language_default_pack: en
updater_config_system_locale: en_US.UTF-8
updater_config_system_language: en_US.UTF-8
```

## Dependencies

_A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles._

## Example Playbook

Example how to use:

```yml
- hosts: servers
  roles:
    - updater
```

## License

GNU AFFERO GENERAL PUBLIC LICENSE

## Author Information

MVladislav
