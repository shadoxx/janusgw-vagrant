# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.hostname = "janusgw"

  config.vm.network "forwarded_port", guest: 80,   host: 8080 #, host_ip: "127.0.0.1"
  config.vm.network "forwarded_port", guest: 8088, host: 8088 #, host_ip: "127.0.0.1"
  config.vm.network "forwarded_port", guest: 7088, host: 7088 #, host_ip: "127.0.0.1"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  config.vm.provision "shell", inline: <<-SHELL
    # Force VM to use the local apt network caching proxy to speed up updates and downloads
    #echo 'Acquire::http::Proxy "http://192.168.42.221:3142";' > /etc/apt/apt.conf.d/proxy

    apt update; apt dist-upgrade -y

    PKGLIST=$(</vagrant/provision/pkglist)
    apt install -y ${PKGLIST[@]}
  SHELL

  config.vm.provision "shell", path: "provision/provision-vm"
end
