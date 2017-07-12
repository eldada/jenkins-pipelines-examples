# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"

  # config.vm.network "forwarded_port", guest: 8000, host: 8000

  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.17.17"

  config.vm.synced_folder ".", "/opt/provisioning"

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false

    # Customize the amount of memory on the VM:
    vb.memory = "4096"
    vb.cpus = 2
  end

  # Install needed tools
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get -qq -y install curl
    curl -sSL https://get.docker.com/ | sh

    # Allow jenkins user to run docker
    usermod -a -G staff,docker vagrant
  SHELL

end