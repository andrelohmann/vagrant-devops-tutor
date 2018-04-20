# -*- mode: ruby -*-
# vi: set ft=ruby :

#require necessary plugins
required_plugins = %w( vagrant-hostmanager vagrant-vbguest vagrant-triggers )
required_plugins.each do |plugin|
  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure(2) do |config|
  # trigger bash script before starting the machine
  #config.trigger.before :up do
  #  run "./trigger.sh"
  #end

  config.vm.box = "ubuntu/xenial64" # 16.04

  # set memory to 2048m
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = "4"
  end

  # auto update guest additions
  config.vbguest.auto_update = true

  # vagrant-hostmanager is necessary to update /etc/hosts on hosts and guests
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.include_offline = true
  config.vm.network "private_network", ip: "192.168.123.123"
  config.vm.hostname = "tutorial-stack.lokal"
  config.hostmanager.aliases = %w(git.tutorial-stack.lokal docker.tutorial-stack.lokal chat.tutorial-stack.lokal runner.tutorial-stack-lokal jenkins.tutorial-stack.lokal mail.tutorial-stack.lokal)

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder "ansible_vagrant", "/vagrant/ansible_vagrant", create: true, owner: "vagrant", group: "vagrant", mount_options: ["dmode=777,fmode=777"]
  config.vm.synced_folder "aws_provisioning/terraform", "/home/vagrant/terraform", create: true, owner: "vagrant", group: "vagrant", mount_options: ["dmode=777,fmode=777"]
  config.vm.synced_folder "aws_provisioning/ansible", "/home/vagrant/ansible", create: true, owner: "vagrant", group: "vagrant", mount_options: ["dmode=777,fmode=777"]

  # Run Ansible from the Vagrant VM
  config.vm.provision "ansible_local" do |ansible|
    ansible.install = true
    ansible.install_mode = :pip
    ansible.version = "latest"
    ansible.playbook = "ansible_vagrant/playbook.yml"
    ansible.galaxy_role_file = "ansible_vagrant/requirements.yml"
  end
end
