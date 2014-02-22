# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Every Vagrant virtual environment requires a box to build off of. Here
  # we are using 64-bit Ubuntu 12.04. It will be fetched from the remote
  # URL if not already installed.
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.35.10"

  # Mount the default synced folder with lax permissions, so as to allow the
  # provisioned nginx user to access it.
  config.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=777", "fmode=766"]

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # For VirtualBox:
  config.vm.provider :virtualbox do |vb|
    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", "512"]
  end

  # Install Nginx.
  config.vm.provision :shell, :inline => "apt-get update && apt-get -y install nginx"
  # Create an nginx user for demonstration purposes.
  config.vm.provision :shell, :inline => "useradd nginx --shell /bin/bash --no-create-home"
end
