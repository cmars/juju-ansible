juju-ansible
============
A simple Ansible plug-in for Juju environments. juju-ansible allows you to use Ansible modules and playbooks with machines you have deployed with Juju.

Why?
----
[Juju](https://juju.ubuntu.com) is unmatched at orchestrating services with complex configuration inter-dependencies that just work.

[Ansible](http://www.ansibleworks.com/docs) is a both simple and powerful tool for distributing ad-hoc, low-level system administration tasks to a large number of machines over ubiquitous SSH.

With their powers combined, you can have opinionated deployments that just work, and then easily go customize and administer them.

Install
-------
Juju and Ansible both need to be installed on your system and in your $PATH.

Then copy 'juju-ansible' into your $PATH.

For playbook support, make a symbolic link 'juju-ansible-playbook' to 'juju-ansible'.

Usage
-----
juju-ansible dynamically creates an inventory file from the status of your current Juju environment. All other arguments are passed on to Ansible:

    $ juju ansible <group> [ansible arguments...]
    $ juju ansible-playbook [ansible-playbook arguments...]

Or send the inventory file to stdout without executing Ansible:

    $ juju ansible --show

Groups are defined for each service. The machines allocated to each service is put in that group. Depending on how you map your services onto machines, these could overlap.

Example
-------
Let's say I have a wordpress and mysql service deployed with Juju in my current environment. I can run Ansible modules like:

    $ juju ansible all -m ping
    $ juju ansible all -m shell -a "uptime"
    $ juju ansible mysql -m shell -a "mysqladmin extended-status"

Or run a playbook (if I created the juju-ansible-playbook symlink above) with:

    $ juju ansible-playbook sched-maint.yml -vvv --sudo

Caveats
-------
I've only tested juju-ansible with an OpenStack Juju environment. YMMV, but let me know how it goes if you try something else.

TODO
----
More groups (by unit, distribution, interface, etc.). Iterating on your much appreciated feedback. What else?

License
-------
GPLv3. Copyright (c) 2013, Canonical Ltd.
