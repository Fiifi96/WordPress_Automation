# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/centos8"
  # config.vm.box = "generic/ubuntu2004"
  config.vm.synced_folder ".", "/vagrant"
  # config.ssh.insert_key = false
  config.vm.provider :virtualbox do |vb|
    vb.memory = 1024
    vb.cpus = 1
    vb.linked_clone = true
  end

  config.vm.define "wordpress" do |wordpress|
    wordpress.vm.hostname = "wordpress.lab"
    wordpress.vm.network "private_network" , ip: "192.168.50.20";
    wordpress.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "rolecheck.yml"
    end
  end

end