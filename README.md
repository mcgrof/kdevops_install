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

Enabling libvirt as a regular user
----------------------------------

kdevops strives to enable a regular user, the user who would use kdevops,
to run libvirt commands as a regular user. This work is handled by the
[https://github.com/mcgrof/libvirt-user](libvirt-user) ansible role.
We use this role twice, once with `only_verify_user` set to False, to
enable the work to get the user to use libvirt as a regular user, and
a second time after with `only_verify_user` set to True so that we can
inform the user if they need to log out and back in. Logging out and
back is required if your user was added to a group.

`install_kdevops` handles this for you. We first enable libvirt to be used
as a regular user in the target `kdevops_vagrant_deps` by running the
[https://github.com/mcgrof/libvirt-user](libvirt-user) ansible role. Then,
on the `kdevops_verify_vagrant_user` target we verify if the user needs to
log out and back in. We do this as a last step.

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
