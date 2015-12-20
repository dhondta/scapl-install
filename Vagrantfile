# -*- mode: ruby -*-
# vi: set ft=ruby :

# IMPORTANT :
#  Don't forget to run the following commands to get the provider plugin installed !
#  $ vagrant plugin install vagrant-vmware-workstation
#  $ vagrant plugin license vagrant-vmware-workstation /path/to/license.lic

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

servers = ['frontend', 'search', 'automation', 'backbone', 'backend']

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "phusion/ubuntu-14.04-amd64"
#  config.vm.box_url = "https://atlas.hashicorp.com/boxcutter/boxes/ubuntu1404/versions/2.0.10/providers/vmware_desktop.box"
  config.vm.box_url = "https://oss-binaries.phusionpassenger.com/vagrant/boxes/latest/ubuntu-14.04-amd64-vmwarefusion.box"

  servers.each do |hostname|
    config.vm.define "#{hostname}" do |server|
      # networking
      case hostname
      when "backbone"
        server.vm.network :private_network, ip: "192.168.1.10"
      when "frontend"
        server.vm.network :private_network, ip: "192.168.1.20"
      when "search"
        server.vm.network :private_network, ip: "192.168.1.30"
      when "automation"
        server.vm.network :private_network, ip: "192.168.1.40"
      when "backend"
        server.vm.network :private_network, ip: "192.168.1.50"
      end

      # customize VM
      server.vm.hostname = "scapl-#{hostname}"
      config.vm.provider :vmware_workstation do |vmware|
        vmware.vmx["name"] = "scapl-#{hostname}"
        case hostname
        when "backbone"
          vmware.vmx["memsize"] = 1024
          vmware.vmx["numvcpus"] = 2
        else
          vmware.vmx["memsize"] = 512
          vmware.vmx["numvcpus"] = 1
        end
      end

      # baseline provisioning
      config.vm.provision "ansible" do |ansible|
        ansible.playbook = "provisioning/scapl-#{hostname}.yml"
        ansible.host_key_checking = false
        ansible.verbose = "v"
      end
    end
  end
end
