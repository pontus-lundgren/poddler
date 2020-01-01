# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # config.vm.box = "generic/fedora28"
  config.vm.box = "f31-cloud-virtualbox"
  config.vm.box_url = "https://ftp.acc.umu.se/mirror/fedora/linux/releases/31/Cloud/x86_64/images/Fedora-Cloud-Base-Vagrant-31-1.9.x86_64.vagrant-virtualbox.box"
  config.ssh.insert_key = false
  # config.vm.box_check_update = false

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  config.vm.network "public_network"
  config.vm.network "private_network", ip: "10.201.5.11", netmask:  "255.255.0.0"

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder ".", "/home/vagrant/devel", type: "sshfs"

  Dir.mkdir('.dnf-cache') unless File.exists?('.dnf-cache')
  config.vm.synced_folder ".dnf-cache", "/var/cache/dnf", type: "sshfs"

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
