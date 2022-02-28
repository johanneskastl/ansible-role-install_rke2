install_rke2
=========

Install rke2 (without downloading and executing shell code with root permissions)

Requirements
------------

None.

Role Variables
--------------

Many.

Basically most options that can be handed over to rke2 when installing via the script being curled and piped to bash, can be set as variables that will be put into the `config.yaml` file.
The only special one is `disable_something` (the CLI option is called `disable`, but that makes a horrible variable name).

If you want to have a specific version of rke2 installed, settings `rke2_version` will do that (see the example playbook below).

In case you want to override the default locations, these two variables can be set:
- `path_to_install_to`: defaults to `/usr/local` or `usr` on RHEL/CentOS/AlmaLinux/RockyLinux
- `systemd_directory_path`: defaults to `/usr/local/lib/systemd/system`

If you know why you would want that, feel free to use a different URL or channel. Here are the defaults:
- `rke2_installation_url`: defaults to `https://update.rke2.io/v1-release/channels`
- `rke2_installation_channel`: defaults to `stable`

Dependencies
------------

None

Example Playbook
----------------

Use a playbook like the following to deploy onto a single node:

```
- hosts: some_hostname
  roles:
    - role: 'johanneskastl.install_rke2'
```

If you want to have a different rke2 version, use something like this:
```
- hosts: some_hostname
  roles:
    - role: 'johanneskastl.install_rke2'
      vars:
        rke2_version: 'v1.22.7+rke2r1'
```

Depending on your host, you might want to set the tls_san variable to contain any external IPs or hostnames or similar.
```
- hosts: some_hostname
  roles:
    - role: 'johanneskastl.install_rke2'
      vars:
        rke2_version: 'v1.22.7+rke2r1'
        tls_san:
          - 'host.example.org'
          - 'k3s.example.org'
          - 'ip-of-loadbalancer-goes-here'
```

Example playbooks for a 'three-server' setup and a 'one server and three agents' can be found here:
- [three-server setup](https://github.com/johanneskastl/rke2_three_servers_with_vagrant_libvirt/blob/main/ansible/playbook-vagrant.yml)
- [one server and three agents](https://github.com/johanneskastl/rke2_one_server_three_agents_with_vagrant_libvirt/blob/main/ansible/playbook-vagrant.yml)

License
-------

BSD-3-Clause

Author Information
------------------

I am Johannes Kastl, reachable via kastl@b1-systems.de.
