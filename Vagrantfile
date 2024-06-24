# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  
  config.vm.define "vmweblb" do |node|
    node.vm.box = "bento/ubuntu-22.04"
    node.vm.hostname = "vmweblb"
    node.vm.network :private_network, ip: "192.168.44.10"
    node.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--groups", "/ProjectA"]
        v.name = "VMWebLB"
        v.memory = 760
        v.cpus = 2
        v.linked_clone = true
    end
  node.vm.provision "shell", privileged: true, path: "./provision/web.sh"
  end

  config.vm.define "vmweb2" do |node|
    node.vm.box = "bento/ubuntu-22.04"
    node.vm.hostname = "vmweb2"
    node.vm.network :private_network, ip: "192.168.44.11"
    node.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--groups", "/ProjectA"]
        v.name = "VMWeb2"
        v.memory = 760
        v.cpus = 2
        v.linked_clone = true
    end
    node.vm.provision "shell", privileged: true, path: "./provision/web.sh"

  end

  config.vm.define "vmwebsockets" do |node|
    node.vm.box = "bento/ubuntu-22.04"
    node.vm.hostname = "vmwebsockets"
    node.vm.network :private_network, ip: "192.168.44.20"
    node.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--groups", "/ProjectA"]
      v.name = "VMWebSockets"
      v.memory = 760
      v.cpus = 2
      v.linked_clone = true
    end
    node.vm.provision "shell", path: "./provision/install_sockets_dependencies.sh"

  end

  config.vm.define "ansible" do |ansible|
    ansible.vm.box = "generic/centos7"
    ansible.vm.hostname = "ansible-server"
    ansible.vm.network "private_network", ip: '192.168.44.30'

    ansible.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--groups", "/ProjectA"]
        v.name = "Ansible-Server"
        v.memory = 760
        # v.linked_clone = true
    end
    ansible.vm.provision "shell", privileged: true, path: "./provision/install_ansible.sh"

    ansible.vm.provision "shell", privileged: false, inline: <<-SHELL
      ssh-keygen -t rsa -N "" -f ~/.ssh/id_rsa
    SHELL

    ansible.vm.synced_folder '.', '/vagrant', disabled: false

  end

  config.vm.define "lb01" do |lb01|
    lb01.vm.box = "bento/ubuntu-22.04"
    lb01.vm.hostname = "lb01"
    lb01.vm.network "private_network", ip: '192.168.44.35'

    lb01.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--groups", "/ProjectA"]
        v.name = "lb01"
        v.memory = 760

        # v.linked_clone = true
    end
    
    lb01.vm.synced_folder '.', '/vagrant', disabled: true
  end


  config.vm.define "vmbasedados" do |node|
    node.vm.box = "bento/ubuntu-22.04"
    node.vm.hostname = "vmbasedados"
    node.vm.network :private_network, ip: "192.168.44.40"
    node.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--groups", "/ProjectA"]
      v.name = "VMBasedados"
      v.memory = 760
      v.cpus = 2
      v.linked_clone = true
    end
    
    node.vm.synced_folder './provision', '/vagrant', disabled: false
    node.vm.provision "shell", path: "./provision/install_database_dependencies_master.sh"

  end

  config.vm.define "vmbasedados2" do |node|
    node.vm.box = "bento/ubuntu-22.04"
    node.vm.hostname = "vmbasedados2"
    node.vm.network :private_network, ip: "192.168.44.41"
    node.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--groups", "/ProjectA"]
      v.name = "VMBasedados2"
      v.memory = 760
      v.cpus = 2
      v.linked_clone = true
    end
    
    node.vm.synced_folder './provision', '/vagrant', disabled: false
    node.vm.provision "shell", path: "./provision/install_database_dependencies_slave.sh"

  end

  config.vm.define "vmpgmanager" do |node|
    node.vm.box = "bento/ubuntu-22.04"
    node.vm.hostname = "vmpgmanager"
    node.vm.network :private_network, ip: "192.168.44.50"
    node.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--groups", "/ProjectA"]
      v.name = "VMPGManager"
      v.memory = 760
      v.cpus = 2
      v.linked_clone = true
    end
    
    node.vm.synced_folder './provision', '/vagrant', disabled: false
    #node.vm.provision "shell", path: "./provision/install_database_dependencies_slave.sh"

  end

  config.vm.define "consul" do |node|
    node.vm.box = "bento/ubuntu-22.04"
    node.vm.hostname = "consul"
    node.vm.network :private_network, ip: "192.168.44.70"
    node.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--groups", "/ProjectA"]
      v.name = "consul-server"
      v.memory = 760
      v.cpus = 2
      v.linked_clone = true
    end

    node.vm.synced_folder '.', '/vagrant', disabled: false

  end



end
