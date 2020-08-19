# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"
  
  config.vm.network "private_network", ip: "192.168.50.4" 

  config.vm.synced_folder "../task", "/task"

    
  config.vm.provider "virtualbox" do |vb|
   # Customize the amount of memory on the VM:
     vb.memory = "512"
   end
end  
  $script = <<-SCRIPT
  #!/bin/bash
# Prerequisites
apt update -y
apt upgrade -y
apt install  apt-transport-https python3-pip dos2unix jq tree -y


# Python 3 Default
update-alternatives --install /usr/bin/python python /usr/bin/python3 10

## Alias
cat > /home/vagrant/.bashrc <<END
  alias python=python3
  alias pip=pip3
  alias ls='ls -la'
END

## Ansible
apt-add-repository -y ppa:ansible/ansible
apt update -y
apt install -y ansible
apt install -y python-pip
apt install -y docker-compose python3
pip3 install ansible-lint
pip uninstall -y docker-py
pip install docker
pip install docker-compose
echo "#############Installing k8s modules#############"
  SCRIPT
  
  Vagrant.configure("2") do |config|
    config.vm.provision "shell", inline: $script
  
  

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "task-playbook.yml"
end
end