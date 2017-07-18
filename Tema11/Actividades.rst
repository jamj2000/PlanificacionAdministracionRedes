Actividades
===========

En términos informáticos, referido a redes, ¿qué es un puerto?
Atendiendo al número de puerto, ¿cómo se clasifican?
¿Qué número de puerto y tipo (TCP, UDP) utilizan los siguientes servidores?
HTTP
HTTPS
DHCP
DNS
SSH
FTP
SMB (Compartición de archivos e impresoras)
MySQL
NTP (Tiempo de red)
BitTorrent
POP3 (Recepción de correo)
IMAP4 (Recepción de correo)
SMTP (Envío de correo)
¿Cuáles son los principales protocolos de la capa de transporte?
Características de UDP.
Características de TCP.
Campos de un segmento TCP. Bits SYN, ACK y FIN.
Cuando abrimos un puerto, ¿qué es una apertura pasiva y qué es una apertura activa?
Proceso de inicio de una conexión TCP.
Proceso de cierre de una conexión TCP.
Cuando se utiliza traducción de direcciones, la traducción de la dirección IP origen se denomina _________________________________
Cuando se utiliza traducción de direcciones, la traducción estática de direcciones se denomina _____________________________
Cuando se utiliza traducción de direcciones, la traducción de la dirección IP destino se denomina ___________________________
Cuando se utiliza traducción de direcciones, la traducción dinámica de direcciones se denomina ____________________________
Si tenemos un router NAT, ¿es posible iniciar una conexión desde Internet a nuestra Intranet a través de él? ¿Por qué? En el caso de que no sea posible, ¿qué debemos hacer para que lo sea?
Tipos de cortafuegos dependiendo del lugar de la red donde se colocan.
Tipos de políticas de los cortafuegos.
¿Qué es el SNAT? ¿Y el enmascaramiento?
¿Qué es el DNAT? Explica cada uno de los siguientes tipos de DNAT:
Port forwarding (redirección de puertos)
Balanceo de carga
Proxy transparente


IPTABLES.
Uso de iptables
iptables -t TABLA -L                      Listado de reglas
iptables -t TABLA -F                      Flush de reglas (borrado total)
 
iptables -t TABLA -P CANAL ACCEPT        Política por defecto permisiva
iptables -t TABLA -P CANAL DROP          Política por defecto restrictiva
 
iptables -t TABLA -A CANAL REGLA          Añadir regla
iptables -t TABLA -D CANAL REGLA          Borrar regla
TABLAS	CANALES o CADENAS
filter	INPUT, FORWARD, OUTPUT
nat	PREROUTING, POSTROUTING
mangle	


REGLAS	SIGNIFICADO
-s IP	Dirección IP origen
-d IP	Dirección IP destino
-i INTERFAZ	Tarjeta de red de entrada. Input
-o INTERFAZ	Tarjeta de red de salida. Output
-p PROTOCOLO	Protocolo (tcp, udp, icmp, ...)
--sport PUERTO	Puerto de origen. Source port
--dport PUERTO	Puerto de destino. Dest. port
-j ACCEPT	Aceptar paquetes
-j DROP	Ignorar paquetes
EJEMPLOS DE REGLAS:

Aceptamos paquetes TCP al puerto 80 desde cualquier IP.
iptables -t filter -A INPUT -s 0.0.0.0/0 -p tcp --dport 80 -j ACCEPT

Bloqueamos paquetes al servidor MySQL
iptables -t filter -A INPUT -p tcp --dport 3306 -j DROP

Permitimos salida a peticiones HTTPS
iptables -t filter -A OUTPUT -p tcp -m tcp --dport 443 -j ACCEPT

Permitimos que los equipos de la red 192.168.10.0 conectados a mi tarjeta eth1 puedan ver páginas web
iptables -t filter -A FORWARD -s 192.168.10.0/24 -i eth1 -p tcp --dport 80 -j ACCEPT

Política de preenrutamiento
iptables -t nat -P PREROUTING ACCEPT

Política de preenrutamiento
iptables -t nat -P POSTROUTING ACCEPT

Todo lo que venga por la tarjeta eth0 y vaya al puerto 80 lo redirigimos a una maquina interna
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j DNAT --to 192.168.10.12:80
 
Todo lo que salga de nuestra red 192.168.10.0 por la tarjeta eth0 se enmascara (es un tipo de SNAT)
iptables -t nat -A POSTROUTING -s 192.168.10.0/24 -o eth0 -j MASQUERADE

Haciendo uso del resumen que aparece arriba y de los ejemplos que aparecen en http://www.pello.info/filez/firewall/iptables.html, ¿cómo escribirías las siguientes reglas?

Hacer un listado de reglas de la tabla filter.
Hacer un listado de reglas de la tabla nat.
Hacer un borrado total (flush) de reglas de la tabla filter.
Hacer un borrado total (flush) de reglas de la tabla nat.
No permitir entrada del equipo 10.0.5.200 al servidor web de nuestro equipo
No permitir entrada del equipo 10.0.5.200 al servidor web 20.20.20.20.
Poner política por defecto ACCEPT para los canales INPUT, FORWARD y OUTPUT.
Poner política por defecto ACCEPT para los canales PREROUTING y POSTROUTING.
Hacer un enmascaramiento de los paquetes de nuestra red 10.0.5.0/24 que salen por eth2. (SNAT)
Todo lo que venga por la tarjeta eth0 destinado al puerto 80 se manda a 10.0.5.222 y puerto 8080. (DNAT)
Ejecuta netstat -na en tu equipo Windows. Muestra una captura de los puertos abiertos.
Ejecuta netstat -punta en un equipo Linux. Muestra una captura de los puertos abiertos.
Ejecuta Zenmap desde un equipo (Windows o Linux). Realiza las siguientes operaciones:
Ver puertos abiertos del equipo 10.0.5.1.
Ver lista de equipos en nuestra subred 10.0.5.0/24.
Ver puertos abiertos de los equipos www.google.es y 8.8.8.8
Hacer un trazado de ruta a los equipos anteriores. Hacer una captura de pantalla donde se muestre la topología.
Hacer un trazado de ruta a www.google.es/30. Hacer una captura de pantalla donde se muestre la topología.
Hacer un pequeño tutorial de configuración de un punto de acceso. (Opcional)
Estado del AP.
Claves de acceso.
Modos de funcionamiento (Repetidor, Bridge, Punto de Acceso, ...)
Configuración de la red Wi-Fi (SSID, Seguridad).
Hacer un pequeño tutorial de configuración de un router.
Estado del router.
Claves de acceso al router.
Configuración de IP Interna / Máscara.
Configuración del DHCP.
Configuración de la red Wi-Fi (SSID, Seguridad) si es un router inalámbrico.
Filtrado de MAC si está disponible.
NAT. Port forwarding. Apertura de puertos.
Hacer un pequeño tutorial de configuración de un switch gestionable si está disponible. (Opcional)
Estado del switch.
Claves de acceso.
Configuración de IP Interna / Máscara.
Configuración de VLANs si está disponible.
¿Qué es y para que sirve un proxy? Ventajas de su uso.
¿Qué diferencias existen entre un proxy normal y uno inverso?
Si tenemos 3 líneas ADSL de distintos ISP y queremos utilizarlas a la vez para nuestra red local para tener una conexión a Internet tolerante a fallos y mayor ancho de banda, ¿qué técnica podemos utilizar?
Tenemos 4 servidores web con el mismo contenido y queremos balancear las peticiones de los clientes entre los 4 servidores. Explica las 2 formas principales de hacerlo.

