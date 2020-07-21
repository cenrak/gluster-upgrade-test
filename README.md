# gluster-upgrade-test
To help work on a 3-node CentOS 7 gluster cluster, running on 1x(1x2) replicas.

## Dependecies:
* [Vagrant](https://www.vagrantup.com/): Vagrant enables users to create and configure lightweight, reproducible, and portable development environments. 
* [Ansible](https://www.ansible.com/): The enterprise solution for building and operating automation at scale

## How to use this repo:
* `git clone https://github.com/cenrak/gluster-upgrade-test.git`:Clone the git repository to your server/workstation 
* `cd gluster-upgrade-test`: Change directory to the local repository directory 
* `vagrant up`: Have Vagrant create the virtual development environment 
* `vagrant ssh-config > config`: Update SSH config file so ansible could easily connect to the virtual machine 
* `ansible-playbook 0-init.yaml`: Initialize your virtual machines 
* `ansible 01-prepare-thick.yaml`: Prepare the virtual machines for the gluster deployment 
* `ansible 02-cluster.yaml`: Setup Gluster cluster 
