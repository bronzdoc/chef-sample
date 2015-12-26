# Defines our Vagrant environment
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # create puppet master node, and lets call it pupo...
  config.vm.define :work_station do |conf|
      conf.vm.box = "ubuntu/trusty64"
      conf.vm.hostname = "workstation"
      conf.vm.network :private_network, ip: "10.0.15.9"
      conf.vm.provider "virtualbox"
      conf.vm.synced_folder "data", "/vagrant"
      conf.vm.provision :shell, inline: <<-SHELL
        sudo apt-get update
        sudo dpkg -i /vagrant/chefdk_0.10.0-1_amd64.deb
        unzip /vagrant/chef-starter.zip
      SHELL
  end

  config.vm.define :chef_server do |conf|
    conf.vm.box = "ubuntu/trusty64"
    conf.vm.hostname = "chefserver"
    conf.vm.network :private_network, ip: "10.0.15.10"
    conf.vm.provider "virtualbox"
  end


  # create some web servers
  config.vm.define "node_1" do |conf|
    conf.vm.box = "ubuntu/trusty64"
    conf.vm.hostname = "node1"
    conf.vm.network :private_network, ip: "10.0.15.21"
    conf.vm.network "forwarded_port", guest: 80, host: "8081"
    conf.vm.provider "virtualbox"
  end

  config.vm.define "node_2" do |conf|
    conf.vm.box = "ubuntu/trusty64"
    conf.vm.hostname = "node2"
    conf.vm.network :private_network, ip: "10.0.15.22"
    conf.vm.network "forwarded_port", guest: 80, host: "8082"
    conf.vm.provider "virtualbox"
  end
end
