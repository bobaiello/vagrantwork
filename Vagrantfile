0# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # config.vm.network "public_network"

  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  # config.vm.box = "ubuntu/trusty64"
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "forwarded_port", guest: 9990, host: 9990,
      auto_correct: true
  config.vm.network "forwarded_port", guest: 8080, host: 8080,
      auto_correct: true

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
  config.vm.define "ansctl" do |ansctl|
    ansctl.vm.box = "ubuntu/trusty64"
    ansctl.vm.hostname = 'ansctl'
    ansctl.vm.box_url = "ubuntu/trusty64"

    ansctl.vm.network :public_network, ip: "192.168.100.100"
    ansctl.vm.network "forwarded_port", guest: 8080, host: 8080,
        auto_correct: true
    ansctl.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--name", "ansctl"]
    end
  end

  config.vm.define "web" do |web|
    web.vm.box = "ubuntu/trusty64"
    web.vm.hostname = 'web'
    web.vm.box_url = "ubuntu/trusty64"

    web.vm.network :public_network, ip: "192.168.100.101"
    web.vm.network "forwarded_port", guest: 9990, host: 9990,
        auto_correct: true
    web.vm.network "forwarded_port", guest: 8080, host: 8080,
        auto_correct: true

    web.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--name", "web"]
    end
  end

  # config.vm.define "db" do |db|
  #   db.vm.box = "ubuntu/trusty64"
  #   db.vm.hostname = 'db'
  #   db.vm.box_url = "ubuntu/trusty64"
  #
  #   db.vm.network :public_network, ip: "192.168.56.102"
  #
  #   db.vm.provider :virtualbox do |v|
  #     v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  #     v.customize ["modifyvm", :id, "--memory", 512]
  #     v.customize ["modifyvm", :id, "--name", "db"]
  #   end
  # end
  # config.vm.define "app" do |app|
  #   app.vm.box = "ubuntu/trusty64"
  #   app.vm.hostname = 'app'
  #   app.vm.box_url = "ubuntu/trusty64"
  #
  #   app.vm.network :public_network, ip: "192.168.56.103"
  #
  #   app.vm.provider :virtualbox do |v|
  #     v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  #     v.customize ["modifyvm", :id, "--memory", 1024]
  #     v.customize ["modifyvm", :id, "--name", "app"]
  #   end
  # end
end
