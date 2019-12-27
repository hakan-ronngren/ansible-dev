# -*- mode: ruby -*-
# vi: set ft=ruby :

# Set up a development machine for Ansible modules, according to
# https://docs.ansible.com/ansible/latest
#     /dev_guide/developing_modules_general.html
#
# After logging on to the virtual machine, get a dev environment:
# . env-setup

require 'fileutils'

# If we have a .gitconfig, we want it in the vm as well
USER_GITCONFIG = File.join(ENV['HOME'], '.gitconfig')
if File.exist?(USER_GITCONFIG)
    FileUtils.cp(USER_GITCONFIG, './.user_gitconfig')
end

Vagrant.configure("2") do |config|
    config.vm.box = "bento/ubuntu-18.04"
    # See if we can use Ubuntu 19.10
    #config.vm.box = "ubuntu/eoan64"

    config.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
    end

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = 'playbook.yaml'
    end
end
