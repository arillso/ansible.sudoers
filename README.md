# Ansible Role: sudoers

<!-- markdownlint-disable MD013 -->

[![license](https://img.shields.io/github/license/mashape/apistatus.svg?style=flat-square&logo=Open%20Source%20Initiative)](LICENSE) [![Ansible Role](https://img.shields.io/ansible/role/54450?label=role%20name&style=flat-square&logo=ansible)](https://galaxy.ansible.com/arillso/sudoers) [![Ansible Role](https://img.shields.io/ansible/role/d/54450.svg?style=flat-square&logo=ansible)](https://galaxy.ansible.com/arillso/sudoers) [![Ansible Quality Score](https://img.shields.io/ansible/quality/54450?label=role%20quality&style=flat-square&logo=ansible)](https://galaxy.ansible.com/arillso/sudoers) [![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/arillso/ansible.sudoers?style=flat-square&logo=github)](https://github.com/arillso/ansible.sudoers/releases) [![GitHub Workflow Status (branch)](https://img.shields.io/github/workflow/status/arillso/ansible.sudoers/Role%20Tests/main?label=integration%20tests&style=flat-square&logo=github)](https://github.com/arillso/ansible.sudoers/actions?query=workflow%3A%22Role+Tests%22)

<!-- markdownlint-enable MD013 -->

## Description

Manage sudoers and sudoers.d in Linux.

## Installation

```bash
ansible-galaxy install arillso.sudoers
```

## Requirements

None

## Role Variables

### sudoers_package

Name of package

```yml
sudoers_package: sudo
```

### sudoers_sudoers

sudores file declarations

```yml
sudoers_sudoers_file: '/etc/sudoers'
```

### sudoers_use_os_defaults

Includes default rules that ship with target distro (boolean)

```yml
sudoers_use_os_defaults: true
```

### sudoers_sudoers

Default configuration options

#### sudoers_sudoers.defaults

default configuration options

```yml
sudoers_sudoers:
  defaults: []
```

#### sudoers_sudoers.defaults_*

Support for additional default types.

Sudoers manual excerpt:

```
Default_Type ::= 'Defaults' |
                 'Defaults' '@' Host_List |
                 'Defaults' ':' User_List |
                 'Defaults' '!' Cmnd_List |
                 'Defaults' '>' Runas_List
```

Variables:

```yml
sudoers_sudoers:
  defaults_host: []
  defaults_user: []
  defaults_cmnd: []
  defaults_runas: []
```

#### sudoers_sudoers.host_aliases

A list of aliases of type `Host_Alias`

| Variable                               | Comments (type)        |
| :------------------------------------- | :--------------------- |
| `sudoers_sudoers.host_aliases.name`:   | Name of the alias      |
| `sudoers_sudoers.host_aliases.members` | Member(s) of the alias |

#### `sudoers_sudoers.user_aliases`

A list of aliases of type `User_Alias`

| Variable                               | Comments (type)        |
| :------------------------------------- | :--------------------- |
| `sudoers_sudoers.user_aliases.name`    | Name of the alias      |
| `sudoers_sudoers.user_aliases.members` | Member(s) of the alias |

#### sudoers_sudoers.cmnd_aliases

A list of aliases of type `Cmnd_Alias`

| Variable                               | Comments (type)        |
| :------------------------------------- | :--------------------- |
| `sudoers_sudoers.cmnd_aliases.name`    | Name of the alias      |
| `sudoers_sudoers.cmnd_aliases.members` | Member(s) of the alias |

#### sudoers_sudoers.runas_aliases

A list of aliases of type `Runas_Alias`

| Variable                                | Comments (type)        |
| :-------------------------------------- | :--------------------- |
| `sudoers_sudoers.runas_aliases.name`    | Name of the alias      |
| `sudoers_sudoers.runas_aliases.members` | Member(s) of the alias |

#### sudoers_sudoers.privileges`

List of privileges

| Variable                           | Comments (type)                                           |
| :--------------------------------- | :-------------------------------------------------------- |
| `sudoers_sudoers.privileges.name`  | Name of user or group (group should be prefixed with '%') |
| `sudoers_sudoers.privileges.entry` | A privilege entry                                         |

### Example

```yml
sudoers_sudoers:
  defaults:
    - env_reset
    - exempt_group=sudo
    - mail_badpass
    - secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
  defaults_host:
    - host_list: SERVERS
      entry: log_year, logfile=/var/log/sudo.log
  defaults_user: 
    - user_list: FULLTIMERS
      entry: '!lecture'
  defaults_cmnd: 
    - cmnd_list: PAGERS
      entry: noexec
  defaults_runas:
    - runas_list: root
      entry: '!set_logname'
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
      entry: 'ALL=(ALL:ALL) ALL'
    - name: '%admin'
      entry: 'ALL=(ALL) ALL'
    - name: '%sudo'
      entry: 'ALL=NOPASSWD:ALL'
```

### sudoers_sudoers_d_files

`/etc/sudoers.d/*` file(s) declarations

### sudoers_sudoers_d_files.key

The name of the sudoers configuration file (e.g `vagrant`)

```yml
sudoers_sudoers_d_files:
  key:
```

| Variable                                            | Default | Comments (type)                                           |
| :-------------------------------------------------- | :------ | :-------------------------------------------------------- |
| `sudoers_sudoers_d_files.key.defaults`              | `[]`    | Default configuration options                             |
| `sudoers_sudoers_d_files.key.defaults_host`         | `[]`    | Defaults@ configuration options                           |
| `sudoers_sudoers_d_files.key.defaults_user`         | `[]`    | Defaults: configuration options                           |
| `sudoers_sudoers_d_files.key.defaults_cmnd`         | `[]`    | Defaults! configuration options                           |
| `sudoers_sudoers_d_files.key.defaults_runas`        | `[]`    | Defaults> configuration options                           |
| `sudoers_sudoers_d_files.key.host_aliases`          | `[]`    | A list of aliases of type `Host_Alias`                    |
| `sudoers_sudoers_d_files.key.host_aliases.name`     |         | Name of the alias                                         |
| `sudoers_sudoers_d_files.key.host_aliases.members`  |         | Member(s) of the alias                                    |
| `sudoers_sudoers_d_files.key.user_aliases`          | `[]`    | A list of aliases of type `User_Alias`                    |
| `sudoers_sudoers_d_files.key.user_aliases.name`     |         | Name of the alias                                         |
| `sudoers_sudoers_d_files.key.user_aliases.members`  |         | Member(s) of the alias                                    |
| `sudoers_sudoers_d_files.key.cmnd_aliases`          | `[]`    | A list of aliases of type `Cmnd_Alias`                    |
| `sudoers_sudoers_d_files.key.cmnd_aliases.name`     |         | Name of the alias                                         |
| `sudoers_sudoers_d_files.key.cmnd_aliases.members`  |         | Member(s) of the alias                                    |
| `sudoers_sudoers_d_files.key.runas_aliases`         | `[]`    | A list of aliases of type `Runas_Alias`                   |
| `sudoers_sudoers_d_files.key.runas_aliases.name`    |         | Name of the alias                                         |
| `sudoers_sudoers_d_files.key.runas_aliases.members` |         | Member(s) of the alias                                    |
| `sudoers_sudoers_d_files.key.privileges`            | `[]`    | List of privileges                                        |
| `sudoers_sudoers_d_files.key.privileges.name`       |         | Name of user or group (group should be prefixed with '%') |
| `sudoers_sudoers_d_files.key.privileges.entry`      |         | A privilege entry                                         |

### Example

```yml
sudoers_sudoers_d_files:
  test:
    defaults:
      - env_reset
      - exempt_group=sudo
      - mail_badpass
      - secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
    defaults_user:
      - user_list: test
        entry: '!authenticate'
    host_aliases:
      - name: WORKSTATIONS
        members: 128.138.0.0/255.255.0.0
    privileges:
      - name: test
        entry: 'ALL=(ALL:ALL) ALL'
```

## Dependencies

None

## Example Playbook

```yaml
---
- hosts: all
  roles:
    - arillso.sudoers
```

## Author

- [Simon Bärlocher](https://sbaerlocher.ch)
- Mark van Driel
- Mischa ter Smitten

## License

This project is under the MIT License. See the [LICENSE](licence) file for the full license text.

## Copyright

(c) 2022, Arillso
