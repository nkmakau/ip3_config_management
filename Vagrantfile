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
    app.vm.hostname = "lx-app-client.client"
    app.vm.network :private_network, ip: "192.168.60.3"
  end

  # Backend App server
  config.vm.define "backend" do |backend|
    backend.vm.hostname = "lx-app-backend.backend"
    backend.vm.network :private_network, ip: "192.168.60.4"
    backend.vm.network "forwarded_port", guest: 5000, host: 5000
  end

  # Mongodb server
  config.vm.define "mongodb" do |mongodb|
    mongodb.vm.hostname = "lx-app-mongodb.mongodb"
    mongodb.vm.network :private_network, ip: "192.168.60.5"
    mongodb.vm.network "forwarded_port", guest: 27017, host: 27017
  end
  
  # Ansible provisioning.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yaml"
  end
end