# Ansible Role: Vulhub

An Ansible role that runs [Vulhub](https://vulhub.org/) environments on a Linux system.

> [!WARNING]
> This role will start multiple vulhub environments (if defined) without checking if they have overlapping port requirements.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    vulhub_git_url: https://github.com/vulhub/vulhub
    vulhub_install_path: /opt/vulhub
    vulhub_branch: master
    vulhub_envs:
    vulhub_persistent: true
    use_local_vulhub_files: false
    local_vulhub_files_path: "{{ playbook_dir | default(omit) }}/roles/ludus_vulhub/files"

## Dependencies

[geerlingguy.docker](https://github.com/geerlingguy/ansible-role-docker)

## Example Playbook

```yaml
- hosts: vulhub_hosts
  roles:
    - badsectorlabs.ludus_vulhub
  vars:
    vulhub_envs:
      - confluence/CVE-2023-22527
      - airflow/CVE-2020-11978
```

## Example Ludus Range Config

```yaml
ludus:
  - vm_name: "{{ range_id }}-vulhub"
    hostname: "{{ range_id }}-vulhub"
    template: debian-12-x64-server-template
    vlan: 20
    ip_last_octet: 1
    ram_gb: 4
    cpus: 2
    linux: true
    testing:
      snapshot: false
      block_internet: false
    roles:
      - badsectorlabs.ludus_vulhub
    role_vars:
      vulhub_envs:
        - confluence/CVE-2023-22527
        - airflow/CVE-2020-11978
```

## Ludus setup

```
ludus ansible roles add badsectorlabs.ludus_vulhub
ludus range config get > config.yml
# Edit config to add the role to the VMs you wish to install vulhub on and define your desired vulhub_envs (see above)
ludus range config set -f config.yml
ludus range deploy -t user-defined-roles
```

## License

GPLv3

## Author Information

This role was created by [Bad Sector Labs](https://badsectorlabs.com/), for [Ludus](https://ludus.cloud/).
