# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  #config.vm.box = "centos/7"
  N = 4
  (1..N).each do |i|
    config.vm.define "server#{i}.gluster.lab" do |server|
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

			if i == N
				server.vm.provision :ansible do |ansible|
					ansible.limit = "all"
					ansible.playbook = "playbook.yml"
					ansible.become = true
					ansible.become_user = "root"
					#ansible.playbook = "inventory.ini"
					ansible.groups = {
						"oldgluster" => ["server[1:2].gluster.lab"],
						"newgluster" => ["server[3:4].gluster.lab"],
						"oldgluster:vars" => {
							"glusterfs_package_full" => "glusterfs-3.7.20",
							"glusterfs_package_name" => "glusterfs-server",
							"glusterfs_package_version" => "3.7.20",
							"glusterfs_repo_baseurl" => "https://download.gluster.org/pub/gluster/glusterfs/old-releases/3.7/3.7.20/CentOS/epel-7/x86_64/"
						},
						"newgluster:vars" => {
              "glusterfs_package_full" => "glusterfs-6.5",
              "glusterfs_package_name" => "glusterfs-server",
              "glusterfs_package_version" => "6.50",
              "glusterfs_repo_baseurl" => "https://buildlogs.centos.org/centos/7/storage/x86_64/gluster-6/"
						}
					}
				end
			end
    end	
	end
end
