# Ansible Role: sshd

## Description

Manage sudoers and sudoers.d in Debian-like systems.

## Installation

```bash
ansible-galaxy install arillso.sudoers
```

## Requirements

None

## Role Variables

| Variable             | Default     | Comments (type)                                   |
| :---                 | :---        | :---                                              |
| `sudoers_sudoers` | `/etc/sudoers` | file declarations |
| `sudoers_sudoers.defaults`| see `defaults/main.yml`   | Default configuration options |
| `sudoers_sudoers.host_aliases`  | `[]`   | A list of aliases of type `Host_Alias` |
| `sudoers_sudoers.host_aliases.name`: | | Name of the alias |
| `sudoers_sudoers.host_aliases.members` | |  Member(s) of the alias |
| `sudoers_sudoers.user_aliases`  | `[]`   | A list of aliases of type `User_Alias` |
| `sudoers_sudoers.user_aliases.name` | | Name of the alias |
| `sudoers_sudoers.user_aliases.members` |  | Member(s) of the alias |
| `sudoers_sudoers.cmnd_aliases`  | `[]`   | A list of aliases of type `Cmnd_Alias` |
| `sudoers_sudoers.cmnd_aliases.name` | | Name of the alias |
| `sudoers_sudoers.cmnd_aliases.members` | | Member(s) of the alias |
| `sudoers_sudoers.runas_aliases`  | `[]`   | A list of aliases of type `Runas_Alias` |
| `sudoers_sudoers.runas_aliases.name` | | Name of the alias |
| `sudoers_sudoers.runas_aliases.members`| | Member(s) of the alias |
| `sudoers_sudoers.privileges`  | see `defaults/main.yml`   | List of privileges |
| `sudoers_sudoers.privileges.name` | | Name of user or group (group should be prefixed with '%')
| `sudoers_sudoers.privileges.entry` | | A privilege entry |
| `sudoers_sudoers_d_files` | `{}`   | `/etc/sudoers.d/*` file(s) declarations |
| `sudoers_sudoers_d_files.key` | | The name of the sudoers configuration file (e.g `vagrant`) |
| `sudoers_sudoers_d_files.key.defaults` | `[]`   | Default configuration options |
| `sudoers_sudoers_d_files.key.host_aliases` | `[]`   | A list of aliases of type `Host_Alias` |
| `sudoers_sudoers_d_files.key.host_aliases.name` | | Name of the alias |
| `sudoers_sudoers_d_files.key.host_aliases.members` | | Member(s) of the alias |
| `sudoers_sudoers_d_files.key.user_aliases` | `[]`   | A list of aliases of type `User_Alias` |
| `sudoers_sudoers_d_files.key.user_aliases.name` | | Name of the alias |
| `sudoers_sudoers_d_files.key.user_aliases.members`| | Member(s) of the alias |
| `sudoers_sudoers_d_files.key.cmnd_aliases` | `[]`   | A list of aliases of type `Cmnd_Alias` |
| `sudoers_sudoers_d_files.key.cmnd_aliases.name` | | Name of the alias |
| `sudoers_sudoers_d_files.key.cmnd_aliases.members` | | Member(s) of the alias |
| `sudoers_sudoers_d_files.key.runas_aliases` | `[]`   | A list of aliases of type `Runas_Alias` |
| `sudoers_sudoers_d_files.key.runas_aliases.name` | | Name of the alias |
| `sudoers_sudoers_d_files.key.runas_aliases.members` | | Member(s) of the alias |
| `sudoers_sudoers_d_files.key.privileges` | `[]`   | List of privileges |
| `sudoers_sudoers_d_files.key.privileges.name` | | Name of user or group (group should be prefixed with '%') |
| `sudoers_sudoers_d_files.key.privileges.entry`| | A privilege entry |
| `sudoers_use_os_defaults` | `True` | Includes default rules that ship with target distro (boolean) |

## Dependencies

None

## Example Playbook

```yaml
---
- hosts: all
  roles:
    - arillso.sudoers
```

### Complex configuration

```yaml
---
- hosts: all
  roles:
    - arillso.sudoers
  vars:
    sudoers_sudoers:
      defaults:
        - env_reset
        - exempt_group=sudo
        - mail_badpass
        - secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
      host_aliases:
        - name: CUNETS
          members: 128.138.0.0/255.255.0.0
        - name: SERVERS
          members: master, mail, www, ns
      user_aliases:
        - name: FULLTIMERS
          members: millert, mikef, dowdy
        - name: PARTTIMERS
          members: bostley, jwfox, crawl
      cmnd_aliases:
        - name: KILL
          members: /usr/bin/kill
        - name: HALT
          members: /usr/sbin/halt
      privileges:
        - name: root
          entry: "ALL=(ALL:ALL) ALL"
        - name: "%admin"
          entry: "ALL=(ALL) ALL"
        - name: "%sudo"
          entry: "ALL=NOPASSWD:ALL"
    sudoers_sudoers_d_files:
      test:
        defaults:
          - env_reset
          - exempt_group=sudo
          - mail_badpass
          - secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
        host_aliases:
          - name: WORKSTATIONS
            members: 128.138.0.0/255.255.0.0
        privileges:
          - name: test
            entry: "ALL=(ALL:ALL) ALL"
```

## Changelog

### 1.2

* Always prepend OS defaults and privileges unless disabled
* fix variables files found

### 1.1

* rename role name
* add new tests

### 1.0

* Initial release

## Author

* [Simon Bärlocher](https://sbaerlocher.ch)
* Mark van Driel
* Mischa ter Smitten

## License

This project is under the MIT License. See the [LICENSE](https://sbaerlo.ch/licence) file for the full license text.

## Copyright

(c) 2018, Simon Bärlocher
