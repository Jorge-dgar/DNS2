# DNS2
Recuperación de DNS


# Iniciar máquinas virtuales
Para poder ejecutar esta práctica es necesario ejecutar el siguiente comando dentro de este directorio:
`$ vagrant up`
Si queremos comprobar si las M.V. se han creado correctamente:
`$ vagrant status`
Una vez confirmamos que se han creado correctamente, entramos por SSH a la máquina DNSA:
`$ vagrant ssh DNSA`

Dentro de DNSA, nos aseguramos de que se han instalado correctamente los paquetes
`$ nslookup -version`
`$ dig -v`
`$ host -v`
`$ systemctl status bind9`

La dirección IP asignada a DNSA es: 192.168.57.10 en la interfaz eth1
La dirección IP asignada a DNSB es: 192.168.57.100 en la interfaz eth1
La dirección IP asignada a cliente es: 192.168.57.200 en la interfaz eth1


Si hacemos ping desde DNSA a DNSB con las IPs especificadas anteriormente, podemos comprobar que se encuentran en la misma red.


# Desarrollo de la práctica
En esta práctica ha sido necesario crear un fichero de zona por cada subdominio especificado en el guión: departamentos, aulas e informática. Además he creado otro fichero de zona para ies.test y para la zona inversa de los mencionados anteriormente.
Es necesario editar los archivos "named.conf.options" y "named.conf.local" para especificar las zonas con las que trabajan ambas MVs.

# Configuración Vagrantfile
He especificado en la creación de DNSA y DNSB que se copien los archivos del apartado anterior, para que al iniciar las máquinas se puedan utilizar directamente.

# Resultados de la práctica
Todas las capturas de pantallas de las pruebas se encuentran en el archivo [pruebas.md](./pruebas.md).