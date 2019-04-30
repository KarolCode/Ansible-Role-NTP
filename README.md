# Ansible Role Install NTP

The use of the role of ansible is the installation of NTP for many Linux distributions

## Supported distributions:

  * Debian
  * Ubuntu
  * CentOS
  * Fedora

## Install role:

### From Ansible Galaxy:

1. Put in to file `galaxy.yml:

```yaml
- name: ntp
  src: karolcode.ntp
  version: "v0.2.0"
```

2. Run command: `ansible-galaxy install -r galaxy.yml`


### From GitHub:

1. Put in to file `galaxy.yml:


```yaml
- name: ntp
  src: https://github.com/KarolCode/Ansible-Role-NTP
  version: "v0.2.0"
```

2. Run command: `ansible-galaxy install -r galaxy.yml`

## Application example:

```yaml
  tasks:

    - name: Install NTP.
      import_role:
        name: ntp
      vars:
        service_is: started   # started / stopped
        when_boot:  disabled  # enabled / disabled
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

### Service management:

Using the ansible role variables `service_is` i `when_boot`, Example:

```yaml
- name: Install NTP.
  import_role:
    name: ntp
  vars:
    service_is: started   # started / stopped
    when_boot:  disabled  # enabled / disabled
```

You can decide whether the service should be started after installation.
You can set whether the service should start the with system start.

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
