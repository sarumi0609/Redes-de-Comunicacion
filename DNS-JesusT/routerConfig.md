# Script configuración router 🌐
***
#### Materia: [[Redes]]
#### Proyecto: [[Actividad1]]
#### Encargado: Jesús Torres
---
```text
enable
configure terminal

! 1. Asignar nombre identificador al router
hostname R1-ConectaBarrio

! 2. Configuracion de la interfaz conectada al Switch principal de la LAN

! Verificar si la interfaz fisica conectada es G0/0/0 o G0/0/1
interface GigabitEthernet0/0/0
 description Conexión a LAN Conecta Barrio
 ip address 192.168.60.1 255.255.255.0
 no shutdown
 exit

! 3. Exclusion de direcciones estaticas del servidor DHCP
! Se excluyen desde la .1 hasta la .99 (cubre router, switches !y los 4 servidores)
ip dhcp excluded-address 192.168.60.1 192.168.60.99

! Se excluyen desde la .221 hasta la .254 para acotar el rango !maximo al .220
ip dhcp excluded-address 192.168.60.221 192.168.60.254

! 4. Creacion y parametrizacion del Pool DHCP
ip dhcp pool POOL_CONECTABARRIO
 network 192.168.60.0 255.255.255.0
 default-router 192.168.60.1
 dns-server 192.168.60.10
 domain-name conectabarrio.local
 exit

! 5. Guardar configuracion en la NVRAM
end
write memory
```
---
