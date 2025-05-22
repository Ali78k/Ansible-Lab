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
sudo apt update
sudo apt install nfs-kernel-server  
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
To install Ansible I use the [latest official documention](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html). for `ubuntu` OS, commands bellow can be used.
```
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

### Ad-Hoc cammands
__1 - PING:__ Ping all inventory nodes.  
```
ansible all -i inventory/hosts.yaml -m ping
```
__2 - LIST:__ Check which commands are going to run in each nodes.
```
ansible-inventory -i inventory/hosts.yaml --list 
```

### Playbooks
To run an examplar scenario, `P01-BootStrap` can be used. It focus on bootstraping a fresh `debian-based` OS, like the condition in `Vagrantfile`.  
So, first of all, run the Vagrant Nodes.
```
vagrant up --provider=libvirt
```
second of all, fill `inventory/hosts.yaml` IP address based on the last providing nodes information. Then, run the ping command. it should see the nodes, and it can connect via ssh and getting `pong` (because of the alternative of `ssh-copy-id` that is implemented in `Vagrantfile`)
```
cd P0-BootStrap
vim inventory/hosts.yaml
ansible-playbook -i inventory/hosts.yaml playbook.yaml  
```
third of all, run the prepared Playbook.  
```
cd P0-BootStrap
ansible-playbook -i inventory/hosts.yaml playbook.yaml  
```
Finally, you can check the logs and use the managed nodes. in this case, `zsh` should be installed.

### Galaxy
There are somewhere to share Ansible roles in the __Galaxy__. `P02-Docker` uses `docker` prepared role to install docker on managed hosts. It is still needed to write a __Playbook__ to call the role like before. This role has many variables to change, accessible [here](https://github.com/geerlingguy/ansible-role-docker#role-variables) - Check `Po2-Docker/inventory/group_vars/all.yaml` as well.    
To get the role, run the command below:  
```
ansible-galaxy install geerlingguy.docker
```
To test the environment, run:  
```
vagrant up --provider=libvirt
cd P02-Docker
ansible all -i inventory/hosts.yaml -m ping
```
And run the playbook:  
```
ansible-playbook -i inventory/hosts.yaml playbook.yaml
```
Now, you can check the VMs via `vagrant ssh <VM-Names>`.  
