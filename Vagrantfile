# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  #config.vm.box = "centos/7"
  N = 3
  (1..N).each do |i|
    config.vm.define "server#{i}" do |server|
      server.vm.box = "centos/7"
      server.vm.network "private_network", ip: "10.0.0.#{i+3}"
      server.vm.hostname = "server#{i}.gluster.lab"

      server.vm.provider "virtualbox" do |vb|
        vb.linked_clone = true

	 			unless File.exist?("./data-server#{i}.vdi")
        	vb.customize ['createhd', '--filename', "./data-server#{i}.vdi", '--size', 10 * 1024]
      	end

      	vb.customize ['storageattach', :id, '--storagectl', 'IDE', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', "./data-server#{i}.vdi"]

      end

    end	
	end
end
