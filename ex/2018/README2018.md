# ASOR - Febrero 2018 - Práctica

*********************** **Ejercicio 1** ***********************

*VM1:

ip link set dev eth0 up
ip addr add 192.168.0.129/25 dev eth0

*RouterA(VM2):

ip link set dev eth0 up
ip link set dev eth1 up

ip addr add 192.168.0.130/25 dev eth0
ip addr add 10.0.0.1/24 dev eth1
</code></pre>

*RouterB(VM3):

ip link set dev eth0 up
$ip link set dev eth1 up

ip addr add 10.0.0.2/24 dev eth1
ip addr add 172.16.0.1/24 dev eth0

*VM1:

ping 192.168.0.130

*VM2:

ping 10.0.2.2



VM2 y VM3:
sysctl -w net.ipv4.conf.all.forwarding=1

nano /etc/quagga/daemons
	zebra=yes
	ripd=yes

nano /etc/quagga/ripd.conf
	router rip
	version 2
	network eth0
	network eth1

service ripd start

vtysh -c "show ip rip"

ip route

 wireshark &

Lo primero que envia es un Request por 224.0.0.9 (y una peticion IGMP para unirse a esa direccion multicast)
Recibe unos primeros response del otro router por multicast
Tras preguntar por ARP a ese router su direccion, este le envia un response por unicast
A partir de aqui se envian actualizaciones por multicast cada tanto, y en pocos mensajes se estabilizan las rutas

VM1:

ip route add default via 192.168.0.130

NOTA: comprobar ping que antes no se alcanzaban


*********************** **Ejercicio 2** ***********************



*********************** **Ejercicio 3** ***********************

