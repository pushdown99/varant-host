# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.synced_folder ".", "/vagrant"
  config.vm.define :ubuntu do |host|
    host.vm.box = "bento/ubuntu-18.04"
    
    host.vm.hostname = "ubuntu"
    config.vm.network "private_network", ip: "169.254.46.99", name: "VirtualBox Host-Only Ethernet Adapter"

    host.vm.disk :disk, size: "10GB", primary: true
    host.vm.provision :shell, path: "bootstrap.sh"

    # Set system settings
    host.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "2048"]
        vb.customize ["modifyvm", :id, "--cpus", "2"]
        vb.customize [ "guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold", 10000 ]
    end
  end
end