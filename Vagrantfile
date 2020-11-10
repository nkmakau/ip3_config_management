# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # General Vagrant VM configuration
  config.vm.box = "geerlingguy/ubuntu2004"
  config.ssh.insert_key = false
  config.vm.provider :virtualbox do |v|
        v.memory = 1024
        v.linked_clone = true
  end

  # Client App server
  config.vm.define "client" do |app|
        app.vm.hostname = "nk-app.client"
        app.vm.network :private_network, ip: "192.168.10.2"
  end

  # Backend App server
  config.vm.define "backend" do |backend|
        backend.vm.hostname = "nk-app.backend"
        backend.vm.network :private_network, ip: "192.168.10.3"
  end

  # Mongodb server
  config.vm.define "mongodb" do |mongodb|
        mongodb.vm.hostname = "nk-app.mongodb"
        mongodb.vm.network :private_network, ip: "192.168.10.4"
  end
  
  # Ansible provisioning.
  config.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbook.yml"
  end
end