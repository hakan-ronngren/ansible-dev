# ansible-dev

Uses [Vagrant](https://www.vagrantup.com/) to create a development environment
for Ansible (not for playbooks etc, but for Ansible itself).

If you are developing a collection, you can share the ansible\_collections
repository with the virtual machine and thus edit files on your host as well
as in the virtual machine.

However, you can't do the same with the Ansible clone, because the Ansible
env-setup scripts create symbolic links, which is a disallowed operation
in the /vagrant mount. Instead, you will get a clone in /home/vagrant.
You will want to add your fork as a remote, or simply change "origin".

To learn about how to extend Ansible, please see the
[Ansible Developer Guide](https://docs.ansible.com/ansible/latest/dev_guide/index.html)
