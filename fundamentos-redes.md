🌐 Fundamentos de Redes para Ciberseguridad (Blue Team)
1. ¿Por qué son importantes las redes en ciberseguridad?
Toda amenaza moderna se comunica por red: exfiltración, C2 (comando y control), movimiento lateral, escaneo, beaconing, etc.

Un buen analista debe detectar comportamientos anómalos, entender protocolos y correlacionar eventos en la red.

2. Modelos de red: OSI y TCP/IP

 Modelo OSI y su relación con la seguridad

Capa	Nombre	Relevancia para Blue Team
7	Aplicación	HTTP, DNS, SSH. Análisis de payloads y cabeceras.
6	Presentación	Cifrado SSL/TLS. Detección de túneles encubiertos.
5	Sesión	Control de sesiones, detección de conexiones ilegítimas.
4	Transporte	TCP/UDP. Escaneos, beaconing, detección de anomalías.
3	Red	IP, ICMP. Análisis de tráfico, geolocalización.
2	Enlace de datos	ARP, MAC spoofing. Man-in-the-Middle (MITM).
1	Física	Menos relevante, pero útil para análisis forense físico.

 Modelo TCP/IP (comparación rápida)

Capa TCP/IP	Equivalente OSI	Ejemplo práctico
Aplicación	5–7 (Sesión a Aplicación)	HTTP, DNS, SMTP, SSH
Transporte	4	TCP, UDP
Internet	3	IP, ICMP
Acceso a red	1–2 (Física y Enlace)	Ethernet, Wi-Fi, ARP

3. Protocolos clave y riesgos asociados

- Protocolo	Puerto	Uso legítimo	                Riesgo común
- DNS	    53	    Resolución de nombres	        Túneles DNS, C2, exfiltración
- HTTP	    80	    Web sin cifrar	                Robo de credenciales, malware
- HTTPS	    443	    Web cifrada	                    Encubrimiento de C2, evasión de IDS mediante cifrado
- SSH	    22	    Acceso remoto	                Fuerza bruta, túneles reversos
- RDP	    3389	Escritorio remoto Windows	    Entrada remota post-compromiso
- ICMP	    N/A	    Ping, traceroute	            Escaneo, covert channels (no usa puertos)
- SMB	    445	    Compartición de archivos	    Movimiento lateral, explotación (EternalBlue)

4. Subredes y segmentación (CIDR)

- Las subredes permiten dividir una red en bloques lógicos, lo cual ayuda a:
- Aislar tráfico por función (ej: usuarios vs. servidores)
- Detectar movimiento lateral
- Aplicar reglas de firewall granulares

Ejemplo práctico

Subred	    Descripción
10.0.0.0/24	Red de servidores
10.0.1.0/24	Red de usuarios internos
10.0.2.0/24	Zona desmilitarizada (DMZ)

Si un usuario de 10.0.1.55 accede a 10.0.0.10 por RDP sin autorización, debe generarse una alerta.

Comando para observar tráfico de una subred
sudo tcpdump -n net 10.0.1.0/24

5. Tipos de tráfico malicioso

Tipo	Ejemplo técnico
Escaneo	nmap -sS 192.168.1.0/24
Beaconing	Conexión periódica a C2 (cada 60 segundos)
Exfiltración	ZIP cifrado enviado vía HTTP POST
Movimiento lateral	Uso de SMB o RDP entre hosts internos
ARP poisoning	Suplantación de gateway mediante ARP

6. Herramientas de análisis de red

Herramienta	    Uso principal
Wireshark	    Análisis profundo de paquetes (PCAP)
tcpdump	        Captura rápida de paquetes por línea de comandos (CLI)
Zeek (Bro)   	Análisis pasivo, logs enriquecidos
Suricata	    IDS/IPS con reglas y alertas
Nmap	        Escaneo de red y fingerprinting
Netstat / ss	Ver conexiones activas

7. Logs relacionados a red

Fuente de log	Qué se ve
Firewall	Tráfico permitido y bloqueado
Proxy	Acceso web, dominios, URLs visitadas
IDS (Suricata)	Alertas sobre firmas conocidas
SIEM	Correlación de eventos por IP/protocolo
Zeek	Conexiones, DNS, HTTP, SSL, etc.

8. Comandos útiles para análisis de red

ss -tulnp                # Ver puertos abiertos y programas asociados
tcpdump -nn -i eth0 port 53  # Capturar tráfico DNS
netstat -ant             # Ver conexiones TCP activas
ip a                     # Ver interfaces de red
ip r                     # Ver rutas configuradas
who                      # Ver usuarios conectados

9. Buenas prácticas para analistas Blue Team

- Segmentar la red por función (servidores, usuarios, DMZ, etc.)
- Bloquear tráfico saliente innecesario
- Monitorear tráfico interno tanto como externo
- Inspeccionar DNS y HTTPS para detectar túneles o C2
- Aplicar reglas de alerta en el IDS/IPS personalizadas
- Mantener registros (logs) por al menos 30 días