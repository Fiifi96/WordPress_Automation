# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/centos8"
  config.vm.synced_folder ".", "/vagrant"
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |vb|
    vb.memory = 1024
    vb.cpus = 1
    vb.linked_clone = true
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.define "wordpress" do |wordpress|
    wordpress.vm.hostname = "wordpress.lab"
    wordpress.vm.network "public_network", bridge: "wlp1s0"
    wordpress.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "wordpress_playbook.yml"
    end
  end

end