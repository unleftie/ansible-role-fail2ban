# Ansible Role for Fail2ban setup

[![CI](https://github.com/unleftie/ansible-role-fail2ban/actions/workflows/ci.yml/badge.svg)](https://github.com/unleftie/ansible-role-fail2ban/actions/workflows/ci.yml)
[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/unleftie/ansible-role-fail2ban/badge)](https://securityscorecards.dev/viewer/?uri=github.com/unleftie/ansible-role-fail2ban)

## Compatibility

| Platform | Version |
| -------- | ------- |
| debian   | 12      |

## Dependencies

- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) (v2.14+)
- [Molecule](https://molecule.readthedocs.io/en/latest/installation.html) + (v4.0.4+) + [docker plugin](https://github.com/ansible-community/molecule-plugins) (for local testing)
- [Docker](https://docs.docker.com/get-docker/) (for local testing)

## Role dependencies

- iptables `required`

## Local Testing

```sh
git clone https://github.com/unleftie/ansible-role-fail2ban.git
cd ansible-role-fail2ban/
molecule test
```

## Installation

> Upgradability notice: When upgrading from old version of this role, be aware that some files may be lost.

```yml
- name: Sample 1
  hosts: all
  become: true
  pre_tasks:
    - name: Ensure apt cache are updated
      apt:
        update_cache: true
        cache_valid_time: 3600
      when: ansible_os_family == "Debian"
  tasks:
    - include_role:
        name: "ansible-role-fail2ban"
```

## 📝 License

This project is licensed under the [MIT](LICENSE).
