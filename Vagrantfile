# encoding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

# SETTINGS

# Box / OS
VAGRANT_BOX = 'ubuntu/trusty64'

# Virtual machine name: <change this>
VM_NAME = 'learning-base'

# Project name: <change this>
PROJECT_NAME = 'learning'

# VM User — 'vagrant' by default
VM_USER = 'vagrant'

# Host folder to sync
HOST_PATH = '.'

# Where to sync to on Guest
GUEST_PATH = '/home/' + VM_USER + '/' + PROJECT_NAME

# VM Port — uncomment this to use NAT instead of DHCP
# VM_PORT = 8080

Vagrant.configure(2) do |config|

  # Box / OS
  config.vm.box = VAGRANT_BOX

  # Virtual machine name
  config.vm.hostname = VM_NAME

  # VM settings
  config.vm.provider "virtualbox" do |v|
    v.name = VM_NAME
    v.gui = false
    v.customize ["modifyvm", :id, "--memory", "2048", "--cpus", "1"]
    v.customize ["modifyvm", :id, "--vram", "32"]
    v.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
  end

  # Port forwarding — uncomment this to use NAT instead of DHCP
  # config.vm.network "forwarded_port", guest: 80, host: VM_PORT

  # DHCP — comment this out if planning on using NAT instead
  config.vm.network "private_network", type: "dhcp"

  # Sync folder
  config.vm.synced_folder HOST_PATH, GUEST_PATH

  # Disable default Vagrant folder, use a unique path per project
  config.vm.synced_folder '.', '/home/'+VM_USER+'', disabled: true

  # Provision: Install Git, Node.js 6.x.x, Latest npm
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
    apt-get install -y nodejs
    apt-get install -y build-essential
    npm install -g npm
    apt-get update
    apt-get upgrade -y
    apt-get autoremove -y
  SHELL
end

    # su vagrant
    # mkdir /home/vagrant/node_modules
    # cd /var/www/project
    # ln -s /home/vagrant/node_modules/ node_modules
