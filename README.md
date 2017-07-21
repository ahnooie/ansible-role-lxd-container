Role Name
=========

This role manages LXD/LXC Containers on a Linux host.

Requirements
------------

LXD 2.0 or greater

Role Variables
--------------

These variables are documented here: http://docs.ansible.com/ansible/latest/lxd_container_module.html

state: started (default), stopped, restarted, absent, frozen
type: image (default)
mode: pull (default)
server: https://images.linuxcontainers.org (default)
protocol: lxd (default)
alias: ubuntu/xenial/amd64 (default)
wait_for_ipv4_addresses: true (default)
timeout: 600 (default)

public_key: "{{ lookup('file','~/.ssh/id_rsa.pub') }}" (default) - path to public ssh key to install in container
install_python: true (default)

enable_ssh: true (default) - installs and enables the openssh server in the container.



Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
