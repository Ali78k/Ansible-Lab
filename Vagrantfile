IMAGE_UBUNTU = "generic/ubuntu2204"
IMAGE_DEBIAN = "debian/bookworm64"

# Set proxy environment for Vagrant itself (only needed if shell uses proxy)
  #  ENV['http_proxy']  = "http://127.0.0.1:2081"
  #  ENV['https_proxy'] = "http://127.0.0.1:2081"
  #  ENV['no_proxy']    = "localhost,127.0.0.1"

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure("2") do |config|
  # Global proxy settings (requires vagrant-proxyconf plugin)
  #   config.proxy.http     = "http://127.0.0.1:2081"
  #   config.proxy.https    = "http://127.0.0.1:2081"
  #   config.proxy.no_proxy = "localhost,127.0.0.1"

  # VM 3: Debian 12
  config.vm.define "debian" do |vm|
    vm.vm.box = IMAGE_DEBIAN
    vm.vm.hostname = "debian"
    #vm.vm.network "private_network", ip: "192.168.56.103"
    vm.vm.provider "libvirt" do |v|
      v.memory = 1024
      v.cpus = 1
    end
    vm.vm.provision "shell", inline: <<-SHELL
      mkdir -p /home/vagrant/.ssh
      echo "#{File.read(File.expand_path('~/.ssh/id_rsa.pub')).strip}" >> /home/vagrant/.ssh/authorized_keys
      chown -R vagrant:vagrant /home/vagrant/.ssh
      chmod 600 /home/vagrant/.ssh/authorized_keys
    SHELL
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
    vm.vm.provision "shell", inline: <<-SHELL
      mkdir -p /home/vagrant/.ssh
      echo "#{File.read(File.expand_path('~/.ssh/id_rsa.pub')).strip}" >> /home/vagrant/.ssh/authorized_keys
      chown -R vagrant:vagrant /home/vagrant/.ssh
      chmod 600 /home/vagrant/.ssh/authorized_keys
    SHELL
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
    vm.vm.provision "shell", inline: <<-SHELL
      mkdir -p /home/vagrant/.ssh
      echo "#{File.read(File.expand_path('~/.ssh/id_rsa.pub')).strip}" >> /home/vagrant/.ssh/authorized_keys
      chown -R vagrant:vagrant /home/vagrant/.ssh
      chmod 600 /home/vagrant/.ssh/authorized_keys
    SHELL
  end
end
