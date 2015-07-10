# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # define this box so Vagrant doesn't call it "default"
  config.vm.define "vagrant-dspace"

  # Hostname for virtual machine
  config.vm.hostname = "dspace.vagrant.dev"

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"
  
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network :forwarded_port, guest: 8080, host: 8080, auto_correct: true
  config.vm.network :forwarded_port, guest: 5432, host: 5432, auto_correct: true
  config.vm.network :forwarded_port, guest: 8443, host: 8443, auto_correct: true

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
  config.vm.synced_folder "dspace-src", "/dspace-src", create: true

  #------------------------------
  # Caching Settings (if enabled)
  #------------------------------
  # BEGIN Vagrant-Cachier (https://github.com/fgrehm/vagrant-cachier) configuration
  # This section will only be triggered if you have installed "vagrant-cachier"
  #   vagrant plugin install vagrant-cachier
  if Vagrant.has_plugin?('vagrant-cachier')
     # Use a vagrant-cachier cache if one is detected
     config.cache.auto_detect = true

     # set vagrant-cachier scope to :box, so other projects that share the
     # vagrant box will be able to used the same cached files
     config.cache.scope = :box

     # and lets specifically use the apt cache (note, this is a Debian-ism)
     config.cache.enable :apt

     # use the generic cache bucket for Maven
     config.cache.enable :generic, {
       "maven" => { cache_dir: "/home/vagrant/.m2/repository" },
     }

     # set the permissions for .m2 so we can use Maven properly
     config.vm.provision :shell, :inline => "chown vagrant:vagrant /home/vagrant/.m2"
  end
  # END Vagrant-Cachier configuration

  # BEGIN Landrush (https://github.com/phinze/landrush) configuration
  # This section will only be triggered if you have installed "landrush"
  #     vagrant plugin install landrush
  if Vagrant.has_plugin?('landrush')
    config.landrush.enable
    # let's use the Google free DNS
    config.landrush.upstream '8.8.8.8'
    config.landrush.guest_redirect_dns = false
  end
  # END Landrush configuration
  
  #-----------------------------
  # Basic System Customizations
  #-----------------------------
  # Check our system locale -- make sure it is set to UTF-8
  # This also means we need to run 'dpkg-reconfigure' to avoid "unable to re-open stdin" errors (see http://serverfault.com/a/500778)
  # For now, we have a hardcoded locale of "en_US.UTF-8"
  locale = "en_US.UTF-8"
  config.vm.provision :shell, :inline => "echo 'Setting locale to UTF-8 (#{locale})...' && locale | grep 'LANG=#{locale}' > /dev/null || update-locale --reset LANG=#{locale} && dpkg-reconfigure locales"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false
  
    # Customize the amount of memory on the VM:
    vb.memory = "2048"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    # locale correct
    sudo locale-gen pt_BR.UTF-8
    # dependencies
    sudo apt-get install -y --force-yes wget unzip 
    # this repository 
    cd ~
    wget https://github.com/royopa/dspace-auto-install/archive/master.zip
    unzip -o master.zip
    cd dspace-auto-install-master
    ./build-dspace
  SHELL
end
