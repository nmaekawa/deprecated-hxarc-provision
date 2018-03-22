# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # vagrant dns; requires `vagrant plugin install landrush`
  config.landrush.enabled = true
  config.landrush.tld = "vm"

  config.vm.define "hxarc" do |hxarc|
    hxarc.vm.box = "bento/ubuntu-16.04"
    hxarc.vm.hostname = "hxarc.vm"
    hxarc.vm.network "private_network", ip: "10.44.0.10"

    hxarc.ssh.forward_agent = true
    hxarc.ssh.insert_key = false

    hxarc.vm.provider "virtualbox" do |v|
        v.memory = "4096"
    end
  end
end
