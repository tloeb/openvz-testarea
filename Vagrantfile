# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.define "openvz"
  config.vm.hostname = "openvz.local"
  config.vm.box = "debian/jessie64"
  config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false  
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
  end

  # View the documentation for the provider you are using for more
  # information on available options.

  # IMPORTANT: We need to seperate the ansible run because during a vagrant provision is no reboot possible
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/init.yml"
    ansible.tags = "stage1"
  end

  config.vm.provision :reload

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/init.yml"
    ansible.tags = ["stage2","stage3"]
  end

  config.vm.provision :reload

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/init.yml"
    ansible.tags = ["stage4"]
    #ansible.tags = ["stage4", "purge"]  If you already provisioned the machine and want to clean it before
  end

end
