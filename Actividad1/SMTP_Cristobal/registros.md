# Hito 1: Implementación Servidor de Correo (SMTP/POP3)

**Universidad de Santiago de Chile (USACH)**
**Asignatura:** Redes de Comunicación
**Profesor:** Juna Iturbe
**Responsable:** Cristóbal

## 1. Objetivo

Configurar y documentar el servidor de correo electrónico de la topología principal para asegurar la comunicación interna entre los hosts, analizando los protocolos de transporte involucrados.

## 2. Direccionamiento y Protocolos

| Dispositivo | Dirección IP | Máscara de Subred | Servicio | Protocolo de Transporte | 
| ----- | ----- | ----- | ----- | ----- | 
| Servidor Correo | 192.168.60.13 | 255.255.255.0 | SMTP / POP3 | TCP (Puertos 25 y 110) | 

**Análisis de Transporte:**
Para este servicio se utilizan los protocolos de aplicación **SMTP** (envío, puerto 25) y **POP3** (recepción, puerto 110). Ambos delegan el envío de los datos a **TCP** en la capa de Transporte.

## 3. Pasos de Configuración en Packet Tracer

1. **Conexión Física:** Se agregó un dispositivo `Server-PT` a la topología, conectado mediante un cable de cobre directo hacia el switch central.

2. **Configuración de Red:** Se ingresó a la interfaz de escritorio del servidor y se le asignó estáticamente la dirección IPv4 `192.168.60.13` con máscara `255.255.255.0`.

3. **Habilitación de Servicios:**

   * Se ingresó a la pestaña *Services > EMAIL* y se encendieron los módulos SMTP y POP3.

   * Se estableció el dominio de red a `correo.com`.

   * Se crearon dos credenciales de prueba para la red: `usuario1` y `usuario2` (ambas con contraseña `123`).

## 4. Pruebas y Resultados

El funcionamiento fue validado mediante dos pruebas de control:

* **Conectividad a nivel de Red:** Se ejecutó el comando `ping 192.168.60.13` desde la terminal de un PC cliente, obteniendo 4 paquetes recibidos con 0% de pérdida, validando la ruta.

* **Prueba de Extremo a Extremo:**

  * Se configuró la herramienta Email del equipo origen con la cuenta de remitente (`usuario1@correo.com`).

  * Se configuró un segundo equipo de la red como receptor (`usuario2@correo.com`).

  * El envío del mensaje desde el remitente indicó *Send Success*, y al ejecutar la acción *Receive* en el equipo destino, el mensaje se desplegó correctamente. Esto confirma que el servidor enruta el tráfico SMTP y POP3 al 100%.

## 5. Entorno de Pruebas Aislado

Para demostrar el correcto funcionamiento de los protocolos sin depender del enrutamiento de la topología principal, se adjunta el archivo `prueba.pkt`. Este contiene una red LAN aislada (1 Switch, 1 Servidor de Correo y 2 PCs cliente) donde se verifica la correcta transmisión y recepción de paquetes SMTP y POP3 de extremo a extremo.