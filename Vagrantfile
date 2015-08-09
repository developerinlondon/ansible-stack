# Defines our Vagrant environment
#
# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

  # create jenkins mgmt node
  config.vm.define :mgmt do |mgmt_config|
      mgmt_config.vm.box = "ubuntu/trusty64"
      mgmt_config.vm.hostname = "mgmt"
      mgmt_config.vm.network :private_network, ip: "10.0.15.10"
      mgmt_config.vm.network "forwarded_port", guest: 9000, host: 9000
      mgmt_config.vm.network "forwarded_port", guest: 3128, host: 3128
      mgmt_config.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
      end
      mgmt_config.vm.synced_folder "roles", "/home/vagrant/roles"
      mgmt_config.vm.synced_folder "inventory", "/home/vagrant/inventory"
      mgmt_config.vm.synced_folder "playbooks", "/home/vagrant/playbooks"
      mgmt_config.vm.synced_folder "library", "/home/vagrant/library"

      mgmt_config.vm.provision :ansible do |ansible|
        ansible.playbook = "playbooks/groups/mgmt.yml"
        ansible.limit = 'all'
      end
  end


  # create load balancer

  config.vm.define :lb do |lb_config|
      lb_config.vm.box = "ubuntu/trusty64"
      lb_config.vm.hostname = "lb"
      lb_config.vm.network :private_network, ip: "10.0.15.11"
      lb_config.vm.network "forwarded_port", guest: 80, host: 8080
      lb_config.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
      end
      #lb_config.vm.provision :ansible do |ansible|
       # ansible.playbook = "playbooks/ssh-addkey.yml"
       # ansible.limit = 'all'
      #  ansible_groups = groups
     #   ansible.inventory_path = "inventory/vagrant.ini"
     # end
  end


  # create some web servers
  # https://docs.vagrantup.com/v2/vagrantfile/tips.html
  (1..3).each do |i|
    config.vm.define "web#{i}" do |node|
        node.vm.box = "ubuntu/trusty64"
        node.vm.hostname = "web#{i}"
        node.vm.network :private_network, ip: "10.0.15.2#{i}"
        node.vm.network "forwarded_port", guest: 80, host: "808#{i}"
        node.vm.provider "virtualbox" do |vb|
          vb.memory = "256"
        end

      #  node.vm.provision :ansible do |ansible|
    #      ansible.playbook = "playbooks/groups/web.yml"
     #     ansible.limit = 'all'
      #    ansible.inventory_path = "inventory/vagrant.ini"
       # end
    end
  end

end
