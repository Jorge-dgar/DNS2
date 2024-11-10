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

La dirección IP asignada a DNSA es: 192.168.2.10 en la interfaz eth1
La dirección IP asignada a DNSB es: 192.168.2.20 en la interfaz eth1
La dirección IP asignada a DNSB es: 192.168.2.30 en la interfaz eth1


Si hacemos ping desde DNSA a DNSB con las IPs especificadas anteriormente, podemos comprobar que se encuentran en la misma red.


# Ejercicios
## Ejercicio 1: Crea el dominio ies.test en DNSA.
1.1 Editar el archivo de configuración de BIND
Accede a la máquina virtual DNSA y abre el archivo de configuración principal de BIND, que generalmente se encuentra en /etc/bind/named.conf.local.