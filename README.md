SCAPL - Installation
====================

Requirements
------------

Ansible >= 1.6

**For Ubuntu**

 `$ sudo apt-get install software-properties-common`
 
 `$ sudo apt-add-repository ppa:ansible/ansible`
 
 `$ sudo apt-get update`
 
 `$ sudo apt-get install ansible`

**Source**: http://docs.ansible.com/ansible/intro_installation.html#latest-releases-via-apt-ubuntu


Steps
-----

Vagrant plugin installation `vagrant-vmware-workstation` plugin is installed and that its `license.lic`

1. Install vagrant plugin for VMWare

 `$ vagrant plugin install vagrant-vmware-workstation`
 
 `$ vagrant plugin license vagrant-vmware-workstation /path/to/license.lic`

2. Clone the Git repository

 `$ git clone https://github.com/dhondta/scapl-install.git`

3. Run Vagrant

 `$ cd scapl-install`

 If you want to install VMs to a specified path:

   `$ mkdir .vagrant && cd .vagrant`

   `$ sudo ln -s /path/to/vm/library machines && cd ..`

  `$ mkdir .vagrant && cd .vagrant`

  `$ sudo ln -s /path/to/vm/library machines && cd ..`

 `$ sudo vagrant up --provider vmware_workstation`


Troubleshooting
---------------

Known problems :

- A warning is thrown regularly telling that "previous known host file not found"

 **Severity**: Low (benign)
 
 **Problem**: No `known_hosts` file exists
 
 **Solution**: `$ touch ~/.ssh/known_hosts`

- An error is thrown telling that the "recursive" attribute is not known for "git" Ansible object

 **Severity**: High (installation crashed)
 
 **Problem**: You're probably running Ansible <1.6 ("recursive" is an attribute added from version 1.6)
 
 **Solution**: Upgrade your Ansible installation

- An error is thrown telling that the "keyserver" attribute is not known for "apt_cache" Ansible object

 **Severity**: High (installation crashed)
 
 **Problem**: You're probably running Ansible <1.6 ("keyserver" is an attribute added from version 1.6)
 
 **Solution**: Upgrade your Ansible installation

- VMs are not installed in VAGRANT_VMWARE_CLONE_DIRECTORY

 **Severity**: Low (benign)

 **Problem**: The VMs are not installed in the path specified via the environment variable VAGRANT_VMWARE_CLONE_DIRECTORY

 **Solution**: This is a known bug from VMWare Workstation ; use a symbolic link instead
