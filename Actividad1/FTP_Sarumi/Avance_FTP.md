# Avance de configuración del protocolo FTP

## 1. Objetivo

Se configuró e implementó un servidor FTP dentro de la red local del proyecto, con el propósito de permitir el almacenamiento y transferencia de materiales asociados a los talleres del centro.

La implementación se realizó sobre la red `192.168.60.0/24`, utilizando la infraestructura

---

## 2. Configuración de red del servidor FTP

El servidor FTP fue incorporado físicamente a la topología mediante una conexión cableada hacia el switch principal de la red.

Se configuró con direccionamiento IPv4 estático utilizando los siguientes parámetros:

| Parámetro | Valor |
|---|---|
| Nombre del dispositivo | `Server_FTP` |
| Dirección IP | `192.168.60.12` |
| Máscara de subred | `255.255.255.0` |
| Puerta de enlace | `192.168.60.1` |
| Servidor DNS | `192.168.60.10` |
| Nombre DNS asociado | `archivos.conectabarrio.local` |

El servidor utiliza una dirección fija debido a que corresponde a un servicio permanente dentro de la LAN y debe poder ser localizado siempre mediante la misma dirección.

---

## 3. Verificación de conectividad

Antes de habilitar el servicio FTP, se verificó la conectividad básica del servidor.

Se realizaron pruebas ICMP desde `Server_FTP` hacia la puerta de enlace:

```text
ping 192.168.60.1
```

La prueba obtuvo 4 respuestas exitosas de 4 paquetes enviados, con 0 % de pérdida.

También se verificó la comunicación con el servidor DNS:

```text
ping 192.168.60.10
```

La prueba obtuvo nuevamente 4 respuestas exitosas de 4 paquetes enviados, con 0 % de pérdida.

Estas pruebas permitieron comprobar que el servidor FTP se encontraba correctamente integrado a la red local.

---

## 4. Habilitación del servicio FTP

En el servidor `Server_FTP` se ingresó a:

`Services > FTP`

El servicio FTP fue habilitado mediante la opción:

```text
Service: On
```

Posteriormente, se creó una cuenta de usuario ficticia destinada a las pruebas del servicio.

### Usuario configurado

| Parámetro | Valor |
|---|---|
| Usuario | `taller` |
| Contraseña | `taller123` |
| Permisos utilizados | Lectura, escritura y listado |

Los permisos permitieron visualizar archivos disponibles, subir archivos al servidor y descargarlos desde un cliente.

---

## 5. Archivo de material de taller

Para demostrar el funcionamiento del servicio se creó un archivo de prueba denominado:

```text
material_taller.txt
```

El archivo contiene información básica relacionada con los talleres de Conecta Barrio y fue utilizado para comprobar las operaciones de transferencia mediante FTP.

---

## 6. Prueba de carga de archivo

Desde un equipo cliente de la LAN se estableció una conexión con el servidor FTP.

Una vez autenticado el usuario, se ejecutó:

```text
put material_taller.txt
```

La transferencia finalizó correctamente:

```text
[Transfer complete - 126 bytes]
```

Posteriormente se utilizó:

```text
dir
```

y se comprobó que el archivo se encontraba almacenado en el servidor:

```text
material_taller.txt    126
```

Con esta prueba se verificó que el usuario configurado posee permisos de escritura y que el servidor permite recibir archivos desde los clientes de la red.

---

## 7. Prueba de descarga de archivo

Para comprobar la transferencia en sentido contrario, se ejecutó:

```text
get material_taller.txt
```

La descarga se realizó correctamente:

```text
[Transfer complete - 126 bytes]
```

Esta prueba confirmó que el servidor permite entregar archivos almacenados a los clientes conectados mediante FTP.

---

## 8. Prueba de acceso mediante DNS

El servicio FTP también fue probado utilizando el nombre registrado en el servidor DNS:

```text
archivos.conectabarrio.local
```

Desde el cliente se ejecutó:

```text
ftp archivos.conectabarrio.local
```

La conexión fue establecida correctamente y el servidor respondió:

```text
Connected to archivos.conectabarrio.local
220- Welcome to PT Ftp server
```

Posteriormente, el usuario `taller` pudo autenticarse correctamente:

```text
230- Logged in
```

Esta prueba permitió verificar la integración entre el servicio DNS y el servidor FTP, evitando la necesidad de ingresar directamente la dirección IP `192.168.60.12`.

---

## 9. Observación preliminar en modo Simulation

Se realizaron observaciones iniciales mediante el modo **Simulation** de Cisco Packet Tracer.

En la secuencia observada se identificó primero una consulta DNS para resolver el nombre:

```text
archivos.conectabarrio.local
```

Posteriormente se observó tráfico TCP entre el cliente y el servidor FTP.

En una de las PDU analizadas se identificaron los siguientes datos:

```text
Origen: PC13
Destino: 192.168.60.12
Protocolo de transporte: TCP
Puerto origen: 1030
Puerto destino: 21
```

Packet Tracer indicó que el cliente enviaba un segmento TCP SYN, correspondiente al inicio del establecimiento de la conexión TCP con el servidor FTP.

También se observó una respuesta FTP desde el servidor hacia el cliente utilizando:

```text
Puerto origen: 21
Puerto destino: 1030
Código FTP: 220
Mensaje: Welcome to PT Ftp server
```

Esto permitió comprobar preliminarmente que el servicio FTP utiliza TCP como protocolo de transporte y que el puerto 21 se utiliza para el canal de control.

---

## 10. Estado actual del avance

La configuración funcional del servicio FTP se encuentra completada para el avance del Hito 1.

Se comprobó satisfactoriamente:

- Conexión física del servidor a la LAN.
- Configuración IPv4 estática.
- Comunicación con la puerta de enlace.
- Comunicación con el servidor DNS.
- Habilitación del servicio FTP.
- Creación de usuario y permisos.
- Carga de archivos mediante `put`.
- Listado de archivos mediante `dir`.
- Descarga de archivos mediante `get`.
- Acceso al servidor mediante el nombre `archivos.conectabarrio.local`.
- Autenticación del usuario FTP.
- Observación inicial del tráfico DNS, TCP y FTP en modo Simulation.

Como actividad de análisis pendiente, se continuará revisando con mayor detalle la secuencia TCP asociada al establecimiento de la conexión, incluyendo la identificación de los segmentos SYN, SYN-ACK y ACK, para incorporarla como evidencia técnica complementaria.

---

## 11. Conclusión preliminar

La implementación realizada permitió dejar operativo el servicio FTP requerido para la red de Conecta Barrio. El servidor fue integrado correctamente a la infraestructura existente y se comprobó tanto la conectividad de red como las operaciones principales de carga y descarga de archivos.

Además, el acceso mediante el nombre `archivos.conectabarrio.local` permitió verificar la correcta relación entre DNS y FTP. Las primeras observaciones en modo Simulation mostraron que la comunicación FTP se establece sobre TCP y utiliza el puerto 21 para el canal de control.
