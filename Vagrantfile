# -*- mode: ruby -*-
# vi: set ft=ruby :


###########################################################################
# See http://docs.vagrantup.com/v2/vagrantfile/index.html for additional
# details on Vagrantfile configuration in general.
###########################################################################

Vagrant.configure("2") do |config|

  config.vm.box = "hashicorp/bionic64"
  config.vm.network "public_network", bridge: "wlp4s0"

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end

  config.ssh.forward_agent = true
  config.vm.synced_folder ".", "/vagrant"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "main.yml"
  end

  config.trigger.after :up do |trigger|
    trigger.info = "Obtaining Public IP"
    trigger.run_remote = {inline: "ip a show dev eth1 | grep -w inet | awk '{print $2}'" }
  end

end
