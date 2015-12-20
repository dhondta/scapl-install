# -*- mode: ruby -*-
# vi: set ft=ruby :

# IMPORTANT :
#  Don't forget to run the following commands to get the provider plugin installed !
#  $ vagrant plugin install vagrant-vmware-workstation
#  $ vagrant plugin license vagrant-vmware-workstation /etc/vmware/<license-file>

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

#servers = ['frontend', 'search', 'automation', 'backbone', 'backend']
servers = ['backbone']
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
        #server.vm.forward_port 22, 5555 # only for development
      when "frontend"
        server.vm.network :private_network, ip: "192.168.1.20"
        #server.vm.forward_port 22, 2222 # only for development
        #server.vm.forward_port 80, 8000
      when "search"
        server.vm.network :private_network, ip: "192.168.1.30"
        #server.vm.forward_port 22, 2222 # only for development
      when "automation"
        server.vm.network :private_network, ip: "192.168.1.40"
        #server.vm.forward_port 22, 2222 # only for development
      when "backend"
        server.vm.network :private_network, ip: "192.168.1.50"
        #server.vm.forward_port 22, 2222 # only for development
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
