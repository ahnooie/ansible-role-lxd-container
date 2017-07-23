Role Name
=========

This role manages LXD/LXC Containers on a remote Linux Container Host.  https://www.ubuntu.com/containers/lxd

Requirements
------------

* LXD 2.0 or greater must be installed on the LXD host and ansible server (it should already be installed by default on Ubuntu 16.04)

* LXD should already be setup on the remote host using `sudo lxd init` or using an Ansible Role such as [juju4/lxd](https://galaxy.ansible.com/juju4/lxd/)

* In order for Ansible to manage an LXD host remotely the following commands must be run ahead of time (from: https://stgraber.org/2016/04/12/lxd-2-0-remote-hosts-and-container-migration-612/

On the remote LXD host:

```
lxc config set core.https_address [::]:8443
lxc config set core.trust_password something-secure
```

On the Ansible host:

```
lxc config set core.https_address [::]:8443
```

```
lxc remote add lxd4 lxd4.example.com
```
(replace lxd4.example.com with the hostname of your LXD host, 'lxd4' can be named whatever you want, you'll need to reference it in the inventory file)

* Ubuntu 16.04 LTS (may work with other distros)

Role Variables
--------------

These variables are documented here: http://docs.ansible.com/ansible/latest/lxd_container_module.html

* `state:` started (default), stopped, restarted, absent, frozen
* `type:` image (default)
* `mode:` pull (default)
* `server:` https://images.linuxcontainers.org (default)
* `protocol:` lxd (default)
* `alias:` ubuntu/xenial/amd64 (default)
* `wait_for_ipv4_addresses:` true (default)
* `timeout:` 600 (default)

Additional Variables:
* `public_key:` "{{ lookup('file','~/.ssh/id_rsa.pub') }}" (default) - path to public ssh key to install in container
* `enable_ssh:` true (default) - installs and enables the openssh server in the container.



Dependencies
------------

None

Example Playbook
----------------

The following example will install 6 containers on the lxd4.example.com LXD host; and on each host install python, add a public ssh key for the root user, install and start the sshd service.

### Inventory File


```
# Remote LXD Host
[lxd]
lxd4.example.com ansible_user=root

# Containers on LXD Hosts
[linux-containers]
ubuntu01.example.com ansible_connection=lxd ansible_host=lxd4:ubuntu01 lxd_host=lxd4.example.com alias=ubuntu/xenial/amd64
ubuntu02.example.com ansible_connection=lxd ansible_host=lxd4:ubuntu02 lxd_host=lxd4.example.com alias=ubuntu/zesty/amd64
centos01.example.com ansible_connection=lxd ansible_host=lxd4:centos01 lxd_host=lxd4.example.com alias=centos/7/amd64
centos02.example.com ansible_connection=lxd ansible_host=lxd4:centos02 lxd_host=lxd4.example.com alias=centos/6/amd64
debian01.example.com ansible_connection=lxd ansible_host=lxd4:debian01 lxd_host=lxd4.example.com alias=debian/stretch/amd64
fedora01.example.com ansible_connection=lxd ansible_host=lxd4:fedora01 lxd_host=lxd4.example.com alias=fedora/25/amd64
```
### Playbook

---
- hosts: linux-containers
  gather_facts: false
  vars:
    public_key: "{{ lookup('file','public_keys/id_rsa.pub') }}"
  roles:
  - lxd-container



License
-------

MIT

Author Information
------------------

Created by [Benjamin Bryan](https://example.com)
