# -*- mode: ruby -*-
# vi: set ft=ruby :

# Prerequisites validation

## Vagrant version
Vagrant.require_version ">= 1.7.4"

## Plugins
unless Vagrant.has_plugin?("vagrant-hostsupdater")
  raise 'Missing vagrant-docker-compose plugin! Make sure to install it by `vagrant plugin install vagrant-hostsupdater`.'
end
unless Vagrant.has_plugin?("vagrant-docker-compose")
  raise 'Missing vagrant-docker-compose plugin! Make sure to install it by `vagrant plugin install vagrant-docker-compose`.'
end

## Variables
$app_name = "vagrant-docker-compose-example.localhost.com"
$coreos_channel = "stable"
$coreos_ip = "192.168.47.100"
$coreos_memory = 1024

# Definitions
Vagrant.configure(2) do |config|
  config.ssh.insert_key = false
  config.vm.hostname = $app_name
  config.vm.box = "coreos-%s" % $coreos_channel
  config.vm.box_version = ">= 766.5.0"
  config.vm.box_url = "http://%s.release.core-os.net/amd64-usr/current/coreos_production_vagrant.json" % $coreos_channel
  
  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--name", $app_name + ".docker.vm"]
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    v.check_guest_additions = false
    v.functional_vboxsf     = false
    v.gui                   = false
    v.memory                = $coreos_memory
    v.cpus                  = 1
  end

  config.vm.network :private_network, ip: $coreos_ip

  config.vm.synced_folder ".", "/home/core/host-data", :nfs => true, :mount_options => ['nolock,vers=3,udp,noatime,actimeo=1']

  ## Avoid plugin conflicts
  if Vagrant.has_plugin?("vagrant-vbguest") then
    config.vbguest.auto_update = false
  end

  config.vm.provision :docker
  
  config.vm.provision :docker_compose,
    compose_version: "1.5.0",
    executable: "/home/core/docker-compose", ## Specifying 'executable' option to avoid CoreOS restriction
    yml: "/home/core/host-data/docker-compose.yml",
    rebuild: false,
    run: "always"
end
