# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile
Vagrant.configure("2") do |config|
  # Configuración de la primera máquina DNSA
  config.vm.define "DNSA" do |dnsa|
    dnsa.vm.box = "debian/bookworm64"        # Box Debian Bookworm
    dnsa.vm.hostname = "dnsa"                # Nombre de la máquina
    dnsa.vm.network "private_network", type: "static", ip: "192.168.57.10", netmask: "255.255.255.0"

    # Copiar archivos de configuración en la mv
    dnsa.vm.provision "file", source: "DNSA_config", destination: "/tmp/DNSA_config"
    # Provisionar BIND y herramientas DNS en DNSA
    dnsa.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y bind9 dnsutils

      # Copiar los archivos de configuración de BIND
      
      cp /tmp/DNSA_config/named.conf.local /etc/bind/named.conf.local
      cp /tmp/DNSA_config/ies.test.dns /etc/bind/ies.test.dns
      cp /tmp/DNSA_config/ies.test.rev /etc/bind/ies.test.rev

      # Eliminar los archivos temporales después de copiarlos
      rm -rf /tmp/DNSA_config
    SHELL
  end

  # Configuración de la segunda máquina DNSB
  config.vm.define "DNSB" do |dnsb|
    dnsb.vm.box = "debian/bookworm64"        # Box Debian Bookworm
    dnsb.vm.hostname = "dnsb"                # Nombre de la máquina
    dnsb.vm.network "private_network", itype: "static", ip: "192.168.57.100", netmask: "255.255.255.0"

     # Copiar archivos de configuración en la mv
    dnsb.vm.provision "file", source: "DNSB_config", destination: "/tmp/DNSB_config"

    # Provisionar BIND y herramientas DNS en DNSB
    dnsb.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y bind9 dnsutils

      # Copiar los archivos de configuración de BIND
      
      cp /tmp/DNSB_config/named.conf.local /etc/bind/named.conf.local
      cp /tmp/DNSB_config/ies.test.dns /etc/bind/ies.test.dns
      cp /tmp/DNSB_config/ies.test.rev /etc/bind/ies.test.rev

    SHELL
  end

  # Configuración de la máquina cliente
  config.vm.define "cliente" do |cliente|
    cliente.vm.box = "debian/bookworm64"        # Box Debian Bookworm
    cliente.vm.hostname = "cliente"                # Nombre de la máquina
    cliente.vm.network "private_network", type: "static", ip: "192.168.2.30", netmask: "255.255.255.0"

    # Provisionar BIND y herramientas DNS en cliente
    cliente.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y bind9 dnsutils
    SHELL
  end
end

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

  # Disable the default share of the current code directory. Doing this
  # provides improved isolation between the vagrant box and your host
  # by making sure your Vagrantfile isn't accessible to the vagrant box.
  # If you use this you may want to enable additional shared subfolders as
  # shown above.
  # config.vm.synced_folder ".", "/vagrant", disabled: true

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
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL

