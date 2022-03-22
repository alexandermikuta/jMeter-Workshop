# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "dajonaga/focaldesktop"
  #config.vm.box = "emoloukanoff/ubuntu-20.04-minimal"
  #config.vm.box = "mhc-cs/Ubuntu-20-04-Xfce"
  #config.vm.box = "mjacobus/ubuntu-20.04-gui"

  # config.vm.provider :virtualbox do |vb|
  #   vb.customize ["modifyvm", :id, "--usb", "on"]
  #   vb.customize ["modifyvm", :id, "--usbehci", "off"]
  #   vb.customize ["modifyvm", :id, "--usbxhci", "off"]
  # end

  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = true

    # Customize the amount of memory on the VM:
    vb.memory = "4096"
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "playbook.yml"
  end
end
