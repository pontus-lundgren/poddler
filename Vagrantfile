# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/centos7"
  # config.ssh.insert_key = false
  # config.vm.box_check_update = false

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  config.vm.network "public_network"
  config.vm.network "private_network", ip: "10.201.5.11", netmask:  "255.255.0.0"

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder ".", "/home/vagrant/devel", type: "sshfs"

#  Dir.mkdir('.yum-cache') unless File.exists?('.yum-cache')
#  config.vm.synced_folder ".yum-cache", "/var/cache/yum", type: "sshfs", create: true, mount_options: ["nonempty"]

  config.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/vagrant-provision.yaml"
  end

  config.vm.define "poddler" do |poddler|
     poddler.vm.host_name = "poddler"
 
     poddler.vm.provider :virtualbox do |domain|
         # Season to taste
#         domain.cpus = 4
#         domain.graphics_type = "spice"
         domain.memory = 2048
#         domain.video_type = "qxl"
     end
  end
end
