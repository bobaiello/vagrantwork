# Bob Aiello
## CM Best Practices Consulting (www.cmbestpractices.com)
## http://www.linkedin.com/in/BobAiello

This repo shows the steps to get Vagrant up and running to support our example
code for learning Ansible.

Use the Vagrantfile (shown below) and run
$ vagrant up

Then you can
$ vagrant ssh ansctl

To update node with ansible
```
$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install ansible
```
Below is the Vagrantfile we used to get started:

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  #First we will start with an Ansible "control" node
  # - so actually this not technically an ansible controller - just a node
  #   we will use to launch our ansible scripts
  config.vm.define "ansctl" do |ansctl|
    ansctl.vm.box = "ubuntu/precise64"
    ansctl.vm.hostname = 'ansctl'
    ansctl.vm.box_url = "ubuntu/precise64"

    ansctl.vm.network :private_network, ip: "192.168.56.100"

    ansctl.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--name", "ansctl"]
    end
  end

  # we define a web server
  config.vm.define "web" do |web|
    web.vm.box = "ubuntu/precise64"
    web.vm.hostname = 'web'
    web.vm.box_url = "ubuntu/precise64"

    web.vm.network :private_network, ip: "192.168.56.101"

    web.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "web"]
    end
  end

  config.vm.define "db" do |db|
    db.vm.box = "ubuntu/precise64"
    db.vm.hostname = 'db'
    db.vm.box_url = "ubuntu/precise64"

    db.vm.network :private_network, ip: "192.168.56.102"

    db.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "db"]
    end
  end
  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/precise64"
    app.vm.hostname = 'app'
    app.vm.box_url = "ubuntu/precise64"

    app.vm.network :private_network, ip: "192.168.56.103"

    app.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--name", "app"]
    end
  end
end
```
