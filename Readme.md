# Ansible Lab
This repository contains some simple examples of ansible, they could be used for any machine I want to start.  
To prepare the Lab, I'm using Vagrant which is a tool to create environments.  

## Up and Running with Vagrant

The first step is installing Vagrant and its dependencies.  
### installing Vagrant
```
wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install vagrant
```
### Installing Dependencies
```
sudo apt install -y vagrant qemu-kvm libvirt-daemon-system libvirt-clients virt-manager
vagrant plugin install vagrant-libvirt
```
### Adding Boxes
This lab will contain two ubuntu hosts and one CentOS machine -- See the `Vagrantfile`. So we can add these box now:
```
vagrant box add generic/ubuntu2204 --provider=libvirt
vagrant box add generic/centos9 --provider=libvirt
```
### Running the Lab Environment
use these commands to run the whole environment
```
vagrant up --provider=libvirt
```
You can access them via ssh
```
vagrant ssh ubuntu1
vagrant ssh ubuntu2
vagrant ssh centos
```
Use `virt-manager` to view or interact with the VMs if needed!  
### Common Tips
- If VMs hang at "Booting from Hard Disk...", try another box like generic/* or enable UEFI.  
- Comment out `private_network` for __libvirt__ unless you configure a custom virtual network.  
- Use `vagrant ssh <vmname>` to enter each VM.  
- Use `vagrant halt`, `vagrant destroy`, `vagrant status` to manage VMs.  
- Use vagrant `global-status` to view all environments.  

## Ansible
### Installing Ansible


### Ad-Hoc cammands

### Playbooks
