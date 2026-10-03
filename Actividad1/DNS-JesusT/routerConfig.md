# Script configuración router 🌐
***
#### Materia: [[Redes]]
#### Proyecto: [[Actividad1]]
#### Encargado: Jesús Torres
---
>Script para la configuración dns y dhcp:

```text
enable
configure terminal

! 1. Asignar nombre identificador al router
hostname R1-ConectaBarrio

! 2. Configuracion de la interfaz conectada al Switch principal de la LAN

! Verificar si la interfaz fisica conectada es G0/0 o G0/1
interface GigabitEthernet0/0
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
>Comprobar en el router que esté funcionando:

```text
! Para ver el estado de la ip al puerto, debe aparecer:
!GigabitEthernet0/0 192.168.60.1 YES manual up up

show ip interface brief
```

```text
! Para ver que funcione el dhcp, debe aparecer:
! Pool POOL_CONECTABARRIO

show ip dhcp pool
```

>Antes de probar en el pc:

```text
C:\>ipconfig /renew
```

>y luego:

```
C:\>ipconfig /all
ping 192.168.60.1
```

El pc debería estar recibiendo correctamente la señal de la red.

> Verificar la asignación en el Router

```
show ip dhcp binding
```