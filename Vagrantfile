# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "vaultserver" do |vaultserver|
	  vaultserver.vm.box = "debian/buster64"
          vaultserver.vm.box_version = "10.0.0"
          vaultserver.vm.synced_folder ".", "/vagrant"
	  vaultserver.vm.provision "ansible" do |ansible|
		  ansible.playbook = "playbooks/playbook-vaultserver.yml"
                  ansible.extra_vars = { ansible_python_interpreter:"/usr/bin/python3" }
	  end
          vaultserver.vm.provider "virtualbox" do |vb|
                  vb.memory = 4096
                  vb.cpus = 3
          end
          vaultserver.vm.provider "libvirt" do |libvirt|
                  libvirt.memory = 4096
                  libvirt.cpus = 3
          end
          vaultserver.vm.network "private_network", ip: "10.0.0.2"
          vaultserver.vm.network "forwarded_port", guest: 30393, host: 30393, auto_correct: true
          vaultserver.vm.network "forwarded_port", guest: 30394, host: 30394, auto_correct: true
  end
end
