# encoding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

# SETTINGS

# Box / OS
VAGRANT_BOX = 'ubuntu/trusty64'

# Virtual machine name: <change this>
VM_NAME = 'myvirtualmachine'

# Project name: <change this>
PROJECT_NAME = 'myproject'

# VM User — 'vagrant' by default
VM_USER = 'vagrant'

# Host folder to sync
HOST_PATH = '.'

# Where to sync to on Guest
GUEST_PATH = '/home/' + VM_USER + '/' + PROJECT_NAME

# VM Port — uncomment this to use NAT instead of DHCP
# VM_PORT = 8080

# Provision script for the Vagrant box
# These commands are run as root
$provision_script = <<SCRIPT

  echo "Install git"
  apt-get update
  apt-get install -y git

  echo "Install node 6.x"
  curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
  apt-get install -y nodejs
  apt-get install -y build-essential
  npm install -g npm

  echo "Update Ubuntu"
  apt-get update
  apt-get upgrade -y
  apt-get autoremove -y

SCRIPT

# Post-provision script for the Vagrant box
# These commands are run as "VM_USER"
$post_provision_script = <<SCRIPT

  echo "Fix the global npm package directory access problem"
  mkdir -p ~/.npm-global-packages
  npm config set prefix "~/.npm-global-packages"

SCRIPT

# Environment variable setup script for the Vagrant box
# These commands are run as "VM_USER"
$profile_setup_script = <<SCRIPT

  ADD_TO_PATH = '~/.npm-global-packages/bin'

  echo "Add needed folders to path"
  [ -f ~/.profile ] || touch ~/.profile
  grep "PATH=$ADD_TO_PATH" ~/.profile \
    || echo "export PATH=$ADD_TO_PATH:"'$PATH' \
    | tee -a ~/.profile
  source ~/.profile

SCRIPT

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

  # Provision: execute commands in $provision_script as root user
  config.vm.provision "shell" do |s|
    s.inline = $provision_script
  end

  # Post-provision: execute commands in $post_provision_script as "VM_USER"
  config.vm.provision "shell" do |s|
    s.inline = $post_provision_script
    s.privileged = false
  end

  # Profile setup: execute commands in $profile_setup_script as "VM_USER"
  config.vm.provision "shell" do |s|
    s.inline = $profile_setup_script
    s.privileged = false
  end

end
