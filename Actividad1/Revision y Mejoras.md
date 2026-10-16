**Riesgos del Hito 1 y mejoras que debemos trabajar** 

| Riesgo identificado | Posible consecuencia | Mejora propuesta |
| ----- | ----- | ----- |
| Wi-Fi abierto | Acceso de usuarios no autorizados e interceptación del tráfico inalámbrico | WPA2-PSK con AES y contraseña robusta |
| HTTP sin cifrado | Exposición de información transmitida | Proponer HTTPS mediante TLS |
| FTP sin cifrado | Exposición de contraseñas y archivos | Proponer SFTP o FTPS |
| Cuenta FTP cisco/cisco | Acceso no autorizado al servidor | Eliminar o deshabilitar la cuenta predeterminada |
| SMTP/POP3 sin cifrado | Exposición de credenciales y mensajes | Proponer SMTP y POP3 protegidos mediante TLS |
| Red única para todos | Mayor posibilidad de acceso entre equipos y propagación de incidentes | Proponer segmentación por VLAN y controles de acceso |

### **Mejoras que implementaremos:** 

1. Proteger el Wi-Fi con WPA2-PSK, comprobar que un cliente autorizado se conecta y recibe una IP mediante DHCP.  
2. Eliminar la cuenta FTP predeterminada `cisco/cisco`, mantener una cuenta específica con los permisos necesarios y verificar que la transferencia sigue funcionando.

Estas modificaciones son relativamente “sencillaa” y  se pueden demostrar en Packet Tracer y permiten comparar la configuración inicial con una versión mejorada.

Para HTTPS, SFTP, FTPS y cifrado del correo, vamos a preparar propuestas técnicas fundamentadas, sin afirmar que se implementaron si el simulador no permite verificar su funcionamiento….

## **Otras mejoras que deberíamos tener en cuenta.** 

Además de los riesgos de seguridad, hay tres puntos que conviene revisar.

***Capacidad de los switches.*** Tres switches de 24 puertos ofrecen 72 puertos físicos, pero también debemos considerar las conexiones hacia el router, los servidores, el punto de acceso y los enlaces entre switches. Hay que comprobar que quedan suficientes puertos para los 60 equipos cableados previstos, no simplemente sumar 24 × 3\.

***Conflicto DHCP.*** En el Hito 1 se detectó un conflicto con `192.168.60.100` y finalmente se asignó `192.168.60.101`. Recomiendo verificar que no existan equipos configurados manualmente dentro del rango DHCP y documentar el comportamiento observado.

***Limitaciones del correo.*** En el informe se explicó que Packet Tracer rechazaba direcciones con el dominio `.local`, por lo que se utilizó `conectabarrio.com` para las cuentas de correo. Mantendría esa solución funcional, explicando claramente la diferencia entre el dominio de correo y el nombre DNS del servidor.

