IMAGE_UBUNTU = "generic/ubuntu2204"
IMAGE_CENTOS = "generic/centos8"  # replaceable with any CentOS-based libvirt box

# Set proxy environment for Vagrant itself (only needed if shell uses proxy)
ENV['http_proxy']  = "http://127.0.0.1:2081"
ENV['https_proxy'] = "http://127.0.0.1:2081"
ENV['no_proxy']    = "localhost,127.0.0.1"

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure("2") do |config|
  # Global proxy settings (requires vagrant-proxyconf plugin)
#  config.proxy.http     = "http://your.proxy.address:port"
#  config.proxy.https    = "http://your.proxy.address:port"
#  config.proxy.no_proxy = "localhost,127.0.0.1"

  # VM 3: CentOS 8 (or compatible)
  config.vm.define "centos" do |vm|
    vm.vm.box = IMAGE_CENTOS
    vm.vm.hostname = "centos"
    #vm.vm.network "private_network", ip: "192.168.56.103"
    vm.vm.provider "libvirt" do |v|
      v.memory = 1024
      v.cpus = 1
    end
  end

  # VM 1: Ubuntu 22.04
  config.vm.define "ubuntu1" do |vm|
    vm.vm.box = IMAGE_UBUNTU
    vm.vm.hostname = "ubuntu1"
    #vm.vm.network "private_network", ip: "192.168.56.101"
    vm.vm.provider "libvirt" do |v|
      v.memory = 1024
      v.cpus = 1
    end
  end

  # VM 2: Ubuntu 22.04
  config.vm.define "ubuntu2" do |vm|
    vm.vm.box = IMAGE_UBUNTU
    vm.vm.hostname = "ubuntu2"
    #vm.vm.network "private_network", ip: "192.168.56.102"
    vm.vm.provider "libvirt" do |v|
      v.memory = 1024
      v.cpus = 1
    end
  end
end
