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

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "hashicorp/precise64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network "forwarded_port", guest: 8080, host: 8080

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
  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.name = "activiti_demo"
    vb.memory = "1024"
    vb.cpus = 2
  end

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
    sudo apt-get install -y wget
    sudo apt-get install -y unzip
    sudo apt-get install -y apache2
    sudo apt-get install -y openjdk-7-jre
    sudo apt-get install -y openjdk-7-jdk

    wget http://apache.go-parts.com/tomcat/tomcat-8/v8.0.24/bin/apache-tomcat-8.0.24.zip
    unzip apache-tomcat-8.0.24.zip -d /opt
    ln -s /opt/apache-tomcat-8.0.24 /opt/tomcat

    groupadd tomcat
    useradd -g tomcat -s /usr/sbin/nologin -m -d /home/tomcat tomcat
    chown -R tomcat:tomcat /opt/apache-tomcat-8.0.24

    echo 'export CATALINA_HOME=/opt/tomcat' >> /etc/profile
    echo 'export CATALINA_BASE=/opt/tomcat' >> /etc/profile

    wget https://github.com/Activiti/Activiti/releases/download/activiti-5.18.0/activiti-5.18.0.zip
    unzip activiti-5.18.0.zip -d /opt
    ln -s /opt/activiti-5.18.0 /opt/activiti

    cp /opt/activiti/wars/activiti-explorer.war /opt/tomcat/webapps
    cp /opt/activiti/wars/activiti-rest.war /opt/tomcat/webapps

    su -p -s /bin/sh tomcat /opt/tomcat/bin/catalina.sh start
  SHELL
end
