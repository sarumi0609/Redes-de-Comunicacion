# Tabla de direccionamiento DNS 🌐
***
#### Materia: [[Redes]]
#### Proyecto: [[Actividad1]]
#### Encargado: Jesús Torres
---
## Datos globales de la red

* **Dirección de red:** `192.168.60.0/24`
* **Máscara de subred:** `255.255.255.0` (Prefijo /24)
* **Dirección de broadcast:** `192.168.60.255`
*  **Gateway:** `192.168.60.1`
* **Servidor DNS principal:** `192.168.60.10`
* **Dominio local:** `conectabarrio.local`
---
## Asignación Estática de Infraestructura y Servidores

| Dispositivo / Rol   | Dirección IP    | Máscara         | Gateway                       | DNS Configurado        | Propósito / Servicio                                     |
| :------------------ | :-------------- | :-------------- | :---------------------------- | :--------------------- | :------------------------------------------------------- |
| **Router (R1)**     | `192.168.60.1`  | `255.255.255.0` | N/A (El router es la gateway) | N/A                    | Gateway de la LAN y Servidor DHCP                        |
| **Servidor DNS**    | `192.168.60.10` | `255.255.255.0` | `192.168.60.1`                | `127.0.0.1`(localhost) | Resolución de nombres de dominio locales                 |
| **Servidor HTTP**   | `192.168.60.11` | `255.255.255.0` | `192.168.60.1`                | `192.168.60.10`        | Portal web informativo (`www.conectabarrio.local`)       |
| **Servidor FTP**    | `192.168.60.12` | `255.255.255.0` | `192.168.60.1`                | `192.168.60.10`        | Repositorio de talleres (`archivos.conectabarrio.local`) |
| **Servidor Correo** | `192.168.60.13` | `255.255.255.0` | `192.168.60.1`                | `192.168.60.10`        | Servicio SMTP/POP3 (`correo.conectabarrio.local`)        |

---
## Distribución y Segmentación del Espacio de Direcciones

| Rango de Direcciones IP             | Cantidad de IPs | Tipo de Asignación | Destino / Justificación                                           |
| :---------------------------------- | :-------------: | :----------------: | :---------------------------------------------------------------- |
| `192.168.60.1`                      |        1        |      Estática      | Asignada a la interfaz del Router (Gateway).                      |
| `192.168.60.2` - `192.168.60.9`     |        8        |  Reserva Estática  | Reserva para switches de administración y Access Point.           |
| `192.168.60.10` - `192.168.60.13`   |        4        |      Estática      | Servidores locales (DNS, Web, FTP, Correo).                       |
| `192.168.60.14` - `192.168.60.99`   |       86        |  Reserva Estática  | Crecimiento futuro de infraestructura y servidores de red.        |
| `192.168.60.100` - `192.168.60.220` |       121       |  Dinámica (DHCP)   | Asignación automática a 48 participantes, 12 personal y 10 Wi-Fi. |
| `192.168.60.221` - `192.168.60.254` |       34        |  Reserva Dinámica  | Rango excluido de respaldo para ampliación de clientes.           |

---
## Justificación de Capacidad del Rango DHCP

* **Demanda proyectada del centro:** 48 equipos de participantes + 12 equipos de personal + 10 dispositivos inalámbricos = **70 clientes simultáneos**.
* **Oferta del pool DHCP (`.100` a `.220`):** 121 direcciones IPv4 disponibles.
* **Margen operativo:** $\frac{121}{70} \approx 172\%$ de cobertura, lo que previene el agotamiento de direcciones durante la rotación de usuarios inalámbricos.

