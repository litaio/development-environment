# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.forward_agent = true
  config.vm.box = "litaio/development-environment"
  config.vm.hostname = "lita-dev"
  config.vm.network "forwarded_port", guest: 8080, host: 8080
end
