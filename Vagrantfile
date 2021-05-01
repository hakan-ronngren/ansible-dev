# -*- mode: ruby -*-
# vi: set ft=ruby :

# Set up a development machine for Ansible modules, according to
# https://docs.ansible.com/ansible/latest
#     /dev_guide/developing_modules_general.html
#
# After logging on to the virtual machine, get a dev environment:
# . env-setup

require 'fileutils'

$ansible_extra_vars = {git: {user: {}}}

['email', 'name'].each do |key|
    str = `git config user.#{key}`.chomp
    if $?.exitstatus == 0
        $ansible_extra_vars[:git][:user][key.to_sym] = str
    end
end

def read_file_into_extra_var(var, path)
    if File.exist?(path)
        $ansible_extra_vars[var.to_sym] = File.read(path)
    end
end

read_file_into_extra_var(:id_rsa_data, File.join(ENV['HOME'], '.ssh', 'id_rsa'))

Vagrant.configure("2") do |config|
    config.vm.box = "bento/ubuntu-21.04"

    config.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
    end

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = 'playbook.yaml'
        ansible.extra_vars = $ansible_extra_vars
    end
end
