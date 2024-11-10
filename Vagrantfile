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

  