# System Updater

[![Ansible Lint](https://github.com/MVladislav/ansible-updater/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/MVladislav/ansible-updater/actions/workflows/ansible-lint.yml)
[![Ansible Molecule Test](https://github.com/MVladislav/ansible-updater/actions/workflows/ci.yml/badge.svg)](https://github.com/MVladislav/ansible-updater/actions/workflows/ci.yml)

- [System Updater](#system-updater)
  - [Role Variables](#role-variables)
  - [Dependencies](#dependencies)
  - [Example Playbook](#example-playbook)
  - [License](#license)

---

You can checkout [MVladislav - ansible-env-setup - playbooks](https://github.com/MVladislav/ansible-env-setup/tree/main/playbooks) for how i use it in general.

Tested with:

- Ubuntu 23.04

## Role Variables

```yml
clients:
  - name: "{{ ansible_user }}"
    locale: en_US.UTF-8
    language: en_US.UTF-8

updater_dependencies:
  - locales
  - tzdata

updater_config:
  set_timezone: true
  set_time_sync: true
  sync_time: true
  set_language: true
  update_upgrade: true
  setup_zfs: false
  setup_unattended: true

updater_time_timezone: Europe/Berlin

updater_ntp_serivce_use:
  timesyncd: false
  chrony: true
updater_ntp_server: time.cloudflare.com
updater_ntp_fallback_server: ntp.ubuntu.com

updater_language_default_pack: en

updater_config_system_locale: en_US.UTF-8
updater_config_system_language: en_US.UTF-8

# multi unattended updater variables
updater_unattended_*: ...
```

## Dependencies

Developed and testes with Ansible 2.14.4

## Example Playbook

Example how to use:

```yml
- name: PRE | pre installer (1) | updater
  remote_user: "{{ ansible_user }}"
  hosts:
    - pre
  roles:
    ### -------------------------
    - role: ansible-updater
      # set language per client
      clients:
        - name: "{{ ansible_user }}"
          locale: en_US.UTF-8
          language: en_US.UTF-8
      # define which modules should be performed
      updater_config:
        set_timezone: true
        set_time_sync: true
        sync_time: true
        set_language: true
        update_upgrade: true
        setup_zfs: true
        setup_unattended: true
      # define your timezone
      updater_time_timezone: Europe/Berlin
      # set ntp servers
      updater_ntp_server: time.cloudflare.com
      updater_ntp_fallback_server: ntp.ubuntu.com
      # set default system language
      updater_language_default_pack: en
      updater_config_system_locale: en_US.UTF-8
      updater_config_system_language: en_US.UTF-8
      # define allowed for unattended to update for
      updater_unattended_allowed_origins:
        # - "Docker:${distro_codename}"
        - "${distro_id}:${distro_codename}"
        - "${distro_id}:${distro_codename}-security"
        - "${distro_id}:${distro_codename}-updates"
        - "${distro_id}ESMApps:${distro_codename}-apps-security"
        - "${distro_id}ESM:${distro_codename}-infra-security"
      # define pattern for unattended to update for
      updater_unattended_origins_patterns:
        # - "o=Docker,a=lunar,l=Docker CE,b=amd64"
        # - "o=Ubuntu,a=${distro_codename},n=${distro_codename},l=Ubuntu"
        - "o=Ubuntu,a=${distro_codename}-security,n=${distro_codename},l=Ubuntu"
        - "o=Ubuntu,a=${distro_codename}-updates,n=${distro_codename},l=Ubuntu"
        # - "o=Ubuntu,a=${distro_codename}-proposed-updates,n=${distro_codename},l=Ubuntu"
        # - "o=Ubuntu,a=${distro_codename}-backports,n=${distro_codename},l=Ubuntu"
```

## License

MIT
