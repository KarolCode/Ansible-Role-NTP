# Ansible Role Install NTP

The use of the role of ansible is the installation of NTP for many Linux distributions

## Supported distributions:

  * Debian
  * Ubuntu
  * CentOS
  * Fedora

## Application example:

```yaml
  tasks:

    - name: Install NTP.
      import_role:
        name: ntp
      tags:
        - ntp
```

## Multi Linux distribution:

### Variable import for many distributions:

This Role of Ansible have support for many Linux distribution and many release,
thanks to cascading inporting variables for Linux distributions.

```yaml
- name: Load the variable tree for distribution
  include_vars: "{{ item }}"
  ignore_errors: yes
  failed_when: false
  with_items:
    - "families/{{ ansible_os_family }}.yml"
    - "distributions/{{ ansible_distribution }}.yml"
    - "releases/{{ ansible_distribution }}-{{ ansible_distribution_major_version}}.yml"
```
The import order of variables:
  1. For the distribution family.
  2. For system distribution.
  3. For major distribution release

Variables are imported sequentially and in case any existing exists, it is replace with a new one.
An attempt to import a non-existent file is skipped and does not return an error.

For example:

```text
├── distributions
│   └── Fedora.yml
├── families
│   ├── Debian.yml
│   └── RedHat.yml
└── releases

```

### Available tasks in the Eole of Ansible:

The ansible role supports additional tasks, by default it is the installation of NTP.

  * `main` - Install NTP daemon (default).
  * `reload` - Reload NTP daemon
  * `enable` - Enable the NTP daemon during the operating system startup.
  * `disable` - Disable the NTP daemon during the operating system startup.
  * `start` - Start NTP daemon
  * `stop` - Stop NTP daemon
  * `restart` - Restart NTP daemon

For example:

```yaml
  - name: Install NTP
      import_role:
        name: ntp
        tasks_from: enable
```
