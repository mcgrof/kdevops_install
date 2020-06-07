kdevops_install
===============

kdevops_install is an ansible role which allows you to lazily deploy all
the requirements for kdevops in one shot. Typically you'd have to manually
update your requirements file and a playbook and respective Makefile target
per role, but this is pretty error prone, and does not allow us to easily
reflect a full release of kdevops.

By using deploying kdevops using a single role we can easily refer to a real
kdevops release, and have that consist of a collection of ansible roles.

Requirements
------------

The following Operating Systems are supported:

  * OS X
  * Linux

Ansible role Variables
----------------------

  * force_kdevops_playbook_dir: set this on your project if your playbooks
    are not in the plabyooks directory.

Dependencies
------------

None.

Example Playbook
----------------

Below is an example playbook, it is used on the kdevops project,
so kdevops/playbooks/kdevops_vagrant.yml file:

```
---
- hosts: localhost
  roles:
    - role: kdevops_install

```

In this particular case note how localhost is used. This is because we are
provisioning the Vagrantfile to the kdevops/vagrant/ directory locally.
You could obviously use a different host.

Further information
--------------------

For further examples refer to one of this role's users, the
[https://github.com/mcgrof/kdevops](kdevops) project or the
[https://github.com/mcgrof/oscheck](oscheck) project from where
this code originally came from.

License
-------

GPLv2
