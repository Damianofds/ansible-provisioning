# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "dhoppe/ubuntu-12.04.5-amd64"
  config.ssh.password = "vagrant"
  config.ssh.insert_key = true
  config.vm.network "private_network", ip: "192.168.66.6"

  config.vm.provider "virtualbox" do |v|
    v.name = "fds-GIS-VM"
    v.memory = 2048
    v.cpus = 2
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
  end
end
