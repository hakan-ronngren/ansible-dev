# ansible-dev

Uses [Vagrant](https://www.vagrantup.com/) to create a development environment
for Ansible (not for playbooks etc, but for Ansible itself).

There is an ansible clone in `~/ansible` and a root directory for collections
in `/vagrant/ansible_collections`.

If you are developing a collection, you can share the ansible\_collections
repository with the virtual machine and thus edit files on your host as well
as in the virtual machine.

However, you can't do the same with the Ansible clone, because the Ansible
env-setup scripts create symbolic links, which is a disallowed operation
in the /vagrant mount. Instead, you will get a clone in /home/vagrant.
You will want to add your fork as a remote, or simply change "origin".

## Usage

Create a group\_vars/all.yaml file to customise your environment. Example:

```yaml
---
ansible_repo: "https://github.com/my-github-name/ansible.git"
checkout_version: "feature/my_feature_branch"
```

Then just start the virtual machine, enter it and source the setup script:

```bash
vagrant up
vagrant ssh
. env-setup
cd ansible
```

It takes a while to pull all docker images required to test your module will
every supported Python version. You may want to do this and take a (long)
break. Unless you already have a module of your own, just pick any built-in
module, such as `copy`.

```bash
ansible-test units --docker --color=yes --requirements <MODULE_NAME>
```

See the [dev guide](https://docs.ansible.com/ansible/latest/dev_guide/testing.html)
for more info on how to test Ansible.

(There is an idea to install a representative set of Python verions, so that
all Ansible tests can run locally, but in the meantime you will have to use
the --docker flag to ansible-test.)

## External links

* [Ansible Developer Guide](https://docs.ansible.com/ansible/latest/dev_guide/index.html)
* [Vagrant Documentation](https://www.vagrantup.com/docs/index.html)
