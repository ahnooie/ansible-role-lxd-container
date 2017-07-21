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
lxc remote add lxd1 203.0.113.2
```
(replace 203.0.113.2 with the IP address or hostname of the LXD host, 'lxd1' can be named whatever you want, but you'll need to reference it in the inventory file)

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

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

MIT

Author Information
------------------

Created by [Benjamin Bryan](https://b3n.org)
