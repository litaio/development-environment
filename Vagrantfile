# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

def host_os
  case RbConfig::CONFIG["host_os"]
  when /darwin/
    :osx
  when /linux/
    :linux
  else
    :unknown
  end
end

def cpu_count
  case host_os
  when :osx
    `sysctl -n hw.ncpu`.to_s.chomp.to_i
  when :linux
    `nproc`.to_s.chomp.to_i
  else
    2
  end
end

def memory
  512
end

Vagrant.configure("2") do |config|
  config.vm.hostname = "lita-dev"
  config.ssh.insert_key = false
  config.vm.box = "coreos-stable"
  config.vm.box_url = "http://stable.release.core-os.net/amd64-usr/current/coreos_production_vagrant.json"

  if Vagrant.has_plugin?("vagrant-vbguest") then
    config.vbguest.auto_update = false
  end

  config.vm.provider :virtualbox do |vb, override|
    vb.memory = memory
    vb.cpus = cpu_count
  end

  [:vmware_fusion, :vmware_workstation].each do |vmware|
    config.vm.provider vmware do |v, override|
      override.vm.box_url = "http://stable.release.core-os.net/amd64-usr/current/coreos_production_vagrant_vmware_fusion.json"
      v.vmx['memsize'] = memory
      v.vmx['numvcpus'] = cpu_count
    end
  end

  config.vm.network :private_network, ip: "172.17.8.254"
  config.vm.synced_folder "docker", "/docker", id: "docker", nfs: true, mount_options: ['nolock,vers=3,udp']
  config.vm.synced_folder "workspace", "/workspace", id: "workspace", nfs: true, mount_options: ['nolock,vers=3,udp']

  config.vm.provision :docker do |docker|
    docker.images = ["litaio/redis:latest", "litaio/ruby:latest"]
  end

  config.vm.provision :file, source: "cloud-config.yml", destination: "/tmp/vagrantfile-user-data"
  config.vm.provision :shell, inline: "mv /tmp/vagrantfile-user-data /var/lib/coreos-vagrant/", privileged: true
end
