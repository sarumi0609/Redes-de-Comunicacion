# Configuración server DNS 🌐
***
#### Materia: [[Redes]]
#### Proyecto: [[Actividad1]]
#### Encargado: Jesús Torres
---
>[!NOTE] El servidor DNS opera en el localhost o 127.0.0.1

![[Pasted image 20261002220507.png]]

>Server-DNS conectado al puerto FastEthernet0/1 del switch0.    

- **Registro 1: Servidor HTTP**        
	- Nombre `www.conectabarrio.local`
	- Address: `192.168.60.11`    
- **Registro 2: Servidor FTP**
	- Nombre: `archivos.conectabarrio.local`
    - Address: `192.168.60.12`
 - **Registro 3: Servidor SMTP/POP3(Correo)**
    - Nombre: `correo.conectabarrio.local`
    - _Address:_ `192.168.60.13`    

>Finalmente en el PC-PT PC-13, ejecutando los siguientes comandos, la conexión funcionó correctamente, además las IPs están en el rango solicitado:
    
```
ipconfig /renew
``` 

```
nslookup www.conectabarrio.local
```
    
   El servidor responde `192.168.60.10` indicando que `www.conectabarrio.local` apunta a `192.168.60.11`_.
   
![[Pasted image 20261002220434.png|640]]

---
