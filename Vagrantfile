$scipt_control = <<-SCRIPT
sudo yum -y install ufw
sed -i "s/.*#host_key_checking.*/host_key_checking = False/g" /etc/ansible/ansible.cfg 
ansible-galaxy collection install community.general
sudo ansible-galaxy collection install community.mysql

SCRIPT

Vagrant.configure("2") do |config|
 
  config.vm.box = "generic/centos8"
  config.vm.synced_folder ".", "/vagrant"
  config.vm.provider "virtualbox" do |v|
    v.linked_clone = true
    v.memory = 1024
    v.cpus = 1
  end  


  config.vm.define "wordpress" do |wordpress|     
    wordpress.vm.hostname = "wordpress"
    wordpress.vm.network "private_network", ip: "192.168.50.11";
    wordpress.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "nginx_playbook.yml"  
    end  
    wordpress.vm.provision "shell" , inline: $scipt_control  
    wordpress.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "open_ports.yml"  
    end
         wordpress.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "mariadb_install.yml"  
    end

    wordpress.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "php_install.yml"  
    end

    wordpress.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "wordpress_playbook.yml"  
    end

  end
  
end    


# config.vm.define "db" do |db|     
#   #   db.vm.hostname = "db"
#   #   #web.vm.network "public_network"
#   #   db.vm.network "private_network", ip: "192.168.50.13";
#   #   db.vm.provision "shell" , inline: $scipt_control
#   #   db.vm.provision "ansible_local" do |ansible|
#   #     ansible.playbook = "dbplaybook.yml"  
#   #   end
    
#   # end

# config.vm.define "control" do |control|     
#   control.vm.hostname = "control"
#   #web.vm.network "public_network"
#   control.vm.network "private_network", ip: "192.168.50.12";
#   control.vm.provision "shell" , inline: $scipt_control
#   control.vm.provision "ansible_local" do |ansible|
#     ansible.playbook = "ansible_install.yml"  
#   end
#   # control.vm.provision "shell" , inline: "sudo cp /vagrant/hosts /etc/ansible/hosts"
# end


#   # wordpress.vm.provision "ansible_local" do |ansible|
#   #   ansible.playbook = "dbplaybook.yml"  
#   # end

#   # wordpress.vm.provision "ansible_local" do |ansible|
#   #   ansible.playbook = "nginx_playbook.yml"  
#   # end
#   # wordpress.vm.provision "ansible_local" do |ansible|
#   #   ansible.playbook = "wordpress_playbook.yml"
#   # end