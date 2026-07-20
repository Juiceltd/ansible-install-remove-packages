# Ansible Role: Install Remove Packages

Small Ansible role for managing package installation and removal on Debian-based hosts.

The role ships with empty defaults, so it does nothing until you provide the package lists you want to manage.

## Requirements

- Ansible 2.14 or newer
- Debian or Ubuntu target hosts
- Privilege escalation for package changes (`become: true`)

## Role Variables

Default variables are defined in `defaults/main.yml`.

```yaml
install_remove_packages_removed: []
install_remove_packages_installed: []
install_remove_packages_extra_removed: []
install_remove_packages_extra_installed: []
```

Use `install_remove_packages_removed` and `install_remove_packages_installed` as the main package lists. The `extra_*` variables are useful when you set a shared baseline elsewhere and want to extend it per host or group.

## Example Playbook

```yaml
---
- name: Manage baseline packages
  hosts: all
  become: true
  roles:
    - role: install_remove_packages
      vars:
        install_remove_packages_removed:
          - snapd
          - popularity-contest
        install_remove_packages_installed:
          - htop
          - ncdu
          - tmux
          - vim
```

## Installation

Install directly from Git:

```yaml
---
roles:
  - src: https://github.com/Juiceltd/ansible-install-remove-packages.git
    name: install_remove_packages
```

Then run:

```shell
ansible-galaxy role install -r requirements.yml
```

## Notes

Package removal uses `purge: true`, so package configuration files are removed as well. Review your remove list before applying the role to existing systems.

The role only runs package tasks on hosts where `ansible_os_family == "Debian"`.

## License

MIT
