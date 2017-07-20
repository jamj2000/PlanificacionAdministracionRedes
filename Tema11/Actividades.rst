Actividades
===========

1. En términos informáticos, referido a redes, ¿qué es un puerto?

2. Atendiendo al número de puerto, ¿cómo se clasifican?

3. ¿Qué número de puerto y tipo (TCP, UDP) utilizan los siguientes servidores?

- HTTP
- HTTPS
- DHCP
- DNS
- SSH
- FTP
- SMB (Compartición de archivos e impresoras)
- MySQL
- NTP (Tiempo de red)
- BitTorrent
- POP3 (Recepción de correo)
- IMAP4 (Recepción de correo)
- SMTP (Envío de correo)

4. ¿Cuáles son los principales protocolos de la capa de transporte?

5. Características de UDP.

6. Características de TCP.

7. Campos de un segmento TCP. Bits SYN, ACK y FIN.

8. Cuando abrimos un puerto, ¿qué es una apertura pasiva y qué es una apertura activa?

9. Proceso de inicio de una conexión TCP.

10. Proceso de cierre de una conexión TCP.

11. Cuando se utiliza traducción de direcciones, la traducción de la dirección IP origen se denomina _________________________________

12. Cuando se utiliza traducción de direcciones, la traducción estática de direcciones se denomina _____________________________

13. Cuando se utiliza traducción de direcciones, la traducción de la dirección IP destino se denomina ___________________________

14. Cuando se utiliza traducción de direcciones, la traducción dinámica de direcciones se denomina ____________________________

15. Si tenemos un router NAT, ¿es posible iniciar una conexión desde Internet a nuestra Intranet a través de él? ¿Por qué? En el caso de que no sea posible, ¿qué debemos hacer para que lo sea?

16. Tipos de cortafuegos dependiendo del lugar de la red donde se colocan.

17. Tipos de políticas de los cortafuegos.

18. ¿Qué es el SNAT? ¿Y el enmascaramiento?

19. ¿Qué es el DNAT? Explica cada uno de los siguientes tipos de DNAT:

 a. Port forwarding (redirección de puertos)
 b. Balanceo de carga
 c. Proxy transparente


**IPTABLES**

 **Uso de iptables**

 .. code-block:: bash

    iptables -t TABLA -L                      # Listado de reglas
    iptables -t TABLA -F                      # Flush de reglas (borrado total)
 
    iptables -t TABLA -P CANAL ACCEPT         # Política por defecto permisiva
    iptables -t TABLA -P CANAL DROP           # Política por defecto restrictiva
 
    iptables -t TABLA -A CANAL REGLA          # Añadir regla
    iptables -t TABLA -D CANAL REGLA          # Borrar regla

 =========== ============================
 TABLAS      CANALES o CADENAS
 =========== ============================
 **filter**  INPUT, FORWARD, OUTPUT
 **nat**     PREROUTING, POSTROUTING
 **mangle**	
 =========== ============================

.

 =============== ==========================
 REGLAS          SIGNIFICADO
 =============== ==========================
 -s IP           Dirección IP origen
 -d IP           Dirección IP destino
 -i INTERFAZ     Tarjeta de red de entrada. Input
 -o INTERFAZ     Tarjeta de red de salida. Output
 -p PROTOCOLO    Protocolo (tcp, udp, icmp, ...)
 --sport PUERTO  Puerto de origen. Source port
 --dport PUERTO  Puerto de destino. Dest. port
 -j ACCEPT       Aceptar paquetes
 -j DROP         Ignorar paquetes
 =============== ==========================

.. note::

   Deberemos sustituir las palabras *TABLA*, *CANAL*, *REGLA*, *IP*, *INTERFAZ*, *PROTOCOLO* y *PUERTO* por los valores adecuados.


**EJEMPLOS DE REGLAS**:

 **Aceptamos paquetes TCP al puerto 80 desde cualquier IP**
 
 .. code-block:: bash
 
    iptables -t filter -A INPUT -s 0.0.0.0/0 -p tcp --dport 80 -j ACCEPT


 **Bloqueamos paquetes al servidor MySQL**
 
 .. code-block:: bash
 
    iptables -t filter -A INPUT -p tcp --dport 3306 -j DROP


 **Permitimos salida a peticiones HTTPS**
  
 .. code-block:: bash
  
    iptables -t filter -A OUTPUT -p tcp -m tcp --dport 443 -j ACCEPT


 **Permitimos que los equipos de la red 192.168.10.0 conectados a mi tarjeta eth1 puedan ver páginas web**
  
 .. code-block:: bash

    iptables -t filter -A FORWARD -s 192.168.10.0/24 -i eth1 -p tcp --dport 80 -j ACCEPT

 **Política de preenrutamiento**


 .. code-block:: bash

    iptables -t nat -P PREROUTING ACCEPT

 **Política de preenrutamiento**

 .. code-block:: bash

    iptables -t nat -P POSTROUTING ACCEPT

 **Todo lo que venga por la tarjeta eth0 y vaya al puerto 80 lo redirigimos a una maquina interna**

 .. code-block:: bash
 
    iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j DNAT --to 192.168.10.12:80
 
 **Todo lo que salga de nuestra red 192.168.10.0 por la tarjeta eth0 se enmascara (es un tipo de SNAT)**
  
 .. code-block:: bash
   
    iptables -t nat -A POSTROUTING -s 192.168.10.0/24 -o eth0 -j MASQUERADE


20 Haciendo uso del resumen que aparece arriba y de los ejemplos que aparecen en http://www.pello.info/filez/firewall/iptables.html, ¿cómo escribirías las siguientes reglas?

 a. Hacer un listado de reglas de la tabla filter.
 b. Hacer un listado de reglas de la tabla nat.
 c. Hacer un borrado total (flush) de reglas de la tabla filter.
 d. Hacer un borrado total (flush) de reglas de la tabla nat.
 e. No permitir entrada del equipo 10.0.5.200 al servidor web de nuestro equipo
 f. No permitir entrada del equipo 10.0.5.200 al servidor web 20.20.20.20.
 g. Poner política por defecto ACCEPT para los canales INPUT, FORWARD y OUTPUT.
 h. Poner política por defecto ACCEPT para los canales PREROUTING y POSTROUTING.
 i. Hacer un enmascaramiento de los paquetes de nuestra red 10.0.5.0/24 que salen por eth2. (SNAT)
 j. Todo lo que venga por la tarjeta eth0 destinado al puerto 80 se manda a 10.0.5.222 y puerto 8080. (DNAT)

21. Ejecuta **netstat -na** en tu equipo Windows. Muestra una captura de los puertos abiertos.

22. Ejecuta **netstat -punta** en un equipo Linux. Muestra una captura de los puertos abiertos.

23. Ejecuta **Zenmap** desde un equipo (Windows o Linux). Realiza las siguientes operaciones:

 a. Ver puertos abiertos del equipo 10.0.5.1.
 b. Ver lista de equipos en nuestra subred 10.0.5.0/24.
 c. Ver puertos abiertos de los equipos www.google.es y 8.8.8.8
 d. Hacer un trazado de ruta a los equipos anteriores. Hacer una captura de pantalla donde se muestre la topología.
 e. Hacer un trazado de ruta a www.google.es/30. Hacer una captura de pantalla donde se muestre la topología.

24. Hacer un pequeño tutorial de configuración de un punto de acceso. (Opcional)

 a. Estado del AP.
 b. Claves de acceso.
 c. Modos de funcionamiento (Repetidor, Bridge, Punto de Acceso, ...)
 d. Configuración de la red Wi-Fi (SSID, Seguridad).

25. Hacer un pequeño tutorial de configuración de un router.

 a. Estado del router.
 b. Claves de acceso al router.
 c. Configuración de IP Interna / Máscara.
 d. Configuración del DHCP.
 e. Configuración de la red Wi-Fi (SSID, Seguridad) si es un router inalámbrico.
 f. Filtrado de MAC si está disponible.
 g. NAT. Port forwarding. Apertura de puertos.

26. Hacer un pequeño tutorial de configuración de un switch gestionable si está disponible. (Opcional)

 a. Estado del switch.
 b. Claves de acceso.
 c. Configuración de IP Interna / Máscara.
 d. Configuración de VLANs si está disponible.

27. ¿Qué es y para que sirve un proxy? Ventajas de su uso.

28. ¿Qué diferencias existen entre un proxy normal y uno inverso?

29. Si tenemos 3 líneas ADSL de distintos ISP y queremos utilizarlas a la vez para nuestra red local para tener una conexión a Internet tolerante a fallos y mayor ancho de banda, ¿qué técnica podemos utilizar?

30. Tenemos 4 servidores web con el mismo contenido y queremos balancear las peticiones de los clientes entre los 4 servidores. Explica las 2 formas principales de hacerlo.

