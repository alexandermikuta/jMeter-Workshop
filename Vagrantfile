# -*- mode: ruby -*-
# vi: set ft=ruby :

IMAGE_NAME = "ubuntu/bionic64"
N_SLAVES = 3

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false

  config.vm.boot_timeout = 3600
  config.ssh.insert_key = false

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end

  config.vm.define "jmeter-master" do |master|
    master.vm.box = IMAGE_NAME
    master.vm.network "private_network", ip: "192.168.50.10"
    master.vm.hostname = "jmeter-master"
    if Vagrant.has_plugin?("vagrant-hosts")
      master.vm.provision :hosts, :sync_hosts => true
    end
    master.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "ansible/tasks/jmeter-master-playbook.yml"
      ansible.extra_vars = {
        ansible_python_interpreter: '/usr/bin/python3',
        node_ip: "192.168.50.10"
      }
    end
    master.vm.provider "virtualbox" do |vb|
      vb.name = "jmeter-master"
    end
  end

  (1..N_SLAVES).each do |i|
    config.vm.define "jmeter-node-#{i}" do |node|
      node.vm.box = IMAGE_NAME
      node.vm.network "private_network", ip: "192.168.50.#{i + 10}"
      node.vm.hostname = "jmeter-node-#{i}"
      if Vagrant.has_plugin?("vagrant-hosts")
        node.vm.provision :hosts, :sync_hosts => true
      end
      node.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "ansible/tasks/jmeter-slave-playbook.yml"
        ansible.extra_vars = {
          ansible_python_interpreter: '/usr/bin/python3',
          node_ip: "192.168.50.#{i + 10}"
        }
      end
      node.vm.provider "virtualbox" do |vb|
        vb.name = "jmeter-node-#{i}"
      end
    end
  end

end