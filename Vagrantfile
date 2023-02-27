# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.hostname = "YOURNAME"
  config.vm.box = "debian/bullseye64"
  config.vm.network "public_network", ip: "YOURIP"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get -y upgrade
  SHELL
end
