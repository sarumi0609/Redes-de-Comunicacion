# Instalación del Servidor HTTP y Access Point 📡

**Materia:** Redes  
**Proyecto:** Actividad1  
**Encargado:** José Ceardi  
**Rol:** Responsable HTTP (Servidor Web, Página del Centro, Pruebas HTTP y Topología)

---

## 1. Servidor HTTP

### 1.1 Datos globales del servidor

| Parámetro                | Valor                   |
| ------------------------ | ----------------------- |
| Nombre del dispositivo   | HTTP                    |
| Dirección IP             | 192.168.60.11           |
| Máscara de subred        | 255.255.255.0 (/24)     |
| Puerta de enlace         | 192.168.60.1            |
| Servidor DNS configurado | 192.168.60.10           |
| Puerto de escucha        | 80 (TCP)                |
| Protocolo de transporte  | TCP                     |
| Nombre de dominio        | www.conectabarrio.local |
| Archivo principal        | index.html              |

### 1.2 documentación RFC de HTTP

#### Según el RFC 9110 (HTTP Semantics):

HTTP vive en la capa de aplicación, o sea, es de los protocolos que usan directamente las aplicaciones como el navegador. Es **sin estado** (stateless), lo que significa que cada petición se procesa sola, sin que el servidor tenga que acordarse de las anteriores. Funciona con un modelo **petición/respuesta**: el cliente pide algo y el servidor le contesta. Está pensado para sistemas donde la información está repartida y se enlaza entre sí (como la web), y en sistemas distribuidos.

**Características principales (RFC 9110):**

- **Stateless:** cada petición se procesa de forma independiente, sin que el servidor guarde memoria de peticiones anteriores.
- **Extensible:** los métodos, códigos de estado y campos (headers) son extensibles.
- **Cliente-servidor:** el cliente envía peticiones; el servidor las responde.
- **Interfaz uniforme:** interfaz genérica para interactuar con cualquier recurso.

**Sintaxis de mensajes (RFC 9112 - HTTP/1.1):**

Un mensaje HTTP/1.1 consiste en:

1. **Start-line** (request-line o status-line)
2. **Headers** (campo: valor)
3. **Línea vacía**
4. **Body** opcional

### 1.3 Infraestructura necesaria

Para que el servidor HTTP funcione en la LAN del centro Conecta Barrio, se requirió:

- **Dispositivo:** 1 Server-PT en Cisco Packet Tracer.
- **Dirección IP fija:** 192.168.60.11 (definida en el enunciado).
- **Máscara:** 255.255.255.0.
- **Puerta de enlace:** 192.168.60.1 (el router).
- **DNS:** 192.168.60.10 (para acceder por nombre).
- **Conexión física:** cable straight-through desde el servidor a un switch.
- **Servicio activo:** HTTP en modo ON.
- **Contenido:** archivo `index.html` con la página informativa del centro.

### 1.4 Pasos de instalación en Packet Tracer

1. **Arrastrar** un Server-PT al área de trabajo.
2. **Renombrar** el dispositivo como `HTTP`.
3. **Conectar** el servidor a un switch con cable straight-through.
4. **Configurar la IP fija:**
   - Desktop → IP Configuration
   - IP: 192.168.60.11
   - Mask: 255.255.255.0
   - Gateway: 192.168.60.1
   - DNS Server: 192.168.60.10
5. **Activar el servicio HTTP:**
   - Services → HTTP → ON
6. **Editar el archivo `index.html`** con contenido informativo del centro.
7. **Guardar** el archivo.
8. **Probar** desde un PC cliente: `http://192.168.60.11`.

### 1.5 Contenido del index.html

```html
<html>
  <head>
    <title>Centro Conecta Barrio</title>
  </head>
  <body>
    <h1>Centro Conecta Barrio</h1>
    <p>Bienvenidos al centro de apoyo digital.</p>
    <h2>Talleres disponibles</h2>
    <ul>
      <li>Computacion basica</li>
      <li>Internet para principiantes</li>
      <li>Correo electronico</li>
    </ul>
    <p>Horario: Lunes a Viernes, 9:00 a 18:00</p>
  </body>
</html>
```
