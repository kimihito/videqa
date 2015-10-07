# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "forwarded_port", guest: 3000, host: 3000

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.33.10"

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
  config.vm.provider "virtualbox" do |vb|
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
    sudo apt-get install -y cmake
    echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" |sudo tee -a  /etc/apt/sources.list.d/pgdg.list
    # install postgresql 9.3
    sudo apt-get install -y postgresql-9.3
    sudo apt-get install -y postgresql-server-dev-9.3
    sudo -u postgres createuser --superuser vagrant
    sudo -u postgres createdb -O vagrant videqa_development
    sudo -u postgres createdb -O vagrant videqa_test
    sudo apt-get install -y postgresql-contrib libpq-dev
    sudo apt-get install -y git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev
    # install ruby 2.1
    sudo add-apt-repository -y ppa:brightbox/ruby-ng
    sudo apt-get update
    sudo apt-get -y install ruby2.1
    sudo apt-get install ruby2.1-dev -y
    # install nodejs
    sudo apt-get install -y nodejs

    # Nokogiri dependencies
    sudo apt-get install -y libxml2 libxml2-dev libxslt1-dev

    # local
    sudo locale-gen ja_JP.UTF-8
    sudo /usr/sbin/update-locale LANG=ja_JP.UTF-8
    cd /vagrant && bundle install
  SHELL
end
