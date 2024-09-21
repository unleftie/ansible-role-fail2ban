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

## Variables

| Variable                        | Description                                                                                     | Value                                                     |
| ------------------------------- | ----------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| `fail2ban_ignoreips`            | Fail2ban will not ban a host which matches an address in this list                              | e.g. "127.0.0.1 192.168.1.0/24"                           |
| `fail2ban_maxretry`             | Number of matches (i.e. value of the counter) which triggers ban action on the IP               |
| `fail2ban_findtime`             | The counter is set to zero if no match is found within "findtime" seconds                       |
| `fail2ban_loglevel`             | Log level output                                                                                | "CRITICAL", "ERROR", "WARNING", "NOTICE", "INFO", "DEBUG" |
| `fail2ban_logtarget`            | Log target                                                                                      | "STDOUT", "STDERR", "SYSLOG", $FILE_PATH                  |
| `fail2ban_syslog_target`        | Syslog file path (if `fail2ban_logtarget` is "SYSLOG")                                          |
| `fail2ban_socket`               | Socket file path                                                                                |
| `fail2ban_pidfile`              | PID file path                                                                                   |
| `fail2ban_dbpurgeage`           | Sets age at which bans should be purged from the database                                       |
| `fail2ban_sendername`           | Sender Name for email notifications                                                             |
| `fail2ban_destemail`            | Destination Email for email notifications                                                       |
| `fail2ban_bantime`              | Duration (in seconds) for IP to be banned for. Negative number for "permanent" ban              |
| `fail2ban_bantime_increment`    | Whether to use database for searching of previously banned IPs                                  | true/false                                                |
| `fail2ban_bantime_factor`       | Bantime increase factor for `fail2ban_bantime_formula`                                          |
| `fail2ban_bantime_formula`      | Formula that will be used to calculate the increased bantime                                    |
| `fail2ban_bantime_overalljails` | Whether to ban IPs for all jails if multiple are defined                                        | true/false                                                |
| `fail2ban_bantime_rndtime`      | Max number of seconds using for mixing with random time to prevent botnets calculate unban time |
| `fail2ban_backend`              | Specifies the backend used to get files modification                                            |
| `fail2ban_banaction`            | Sets the global/default banaction                                                               |
| `fail2ban_mta`                  | Email notifications action                                                                      |
| `fail2ban_protocol`             | Sets the default protocol                                                                       |
| `fail2ban_chain`                | Specifies the chain where jumps would need to be added in iptables-\* actions                   |
| `fail2ban_action`               | An action defines several commands which are executed at different moments                      |
| `fail2ban_services`             | Name of the service to be used by the jail to detect matches                                    |

## 📝 License

This project is licensed under the [MIT](LICENSE).
