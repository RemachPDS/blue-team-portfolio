Fundamentos de Criptografía

Este documento resume los conceptos esenciales de criptografía aplicados a la ciberseguridad. Comprender estos principios permite proteger la confidencialidad, integridad y autenticidad de los datos en entornos corporativos.

1. ¿Por qué es importante la criptografía en ciberseguridad?

La criptografía es fundamental para:

    Proteger la información en tránsito (ej. HTTPS, VPNs)

    Proteger datos en reposo (bases de datos, discos, backups)

    Verificar la identidad (autenticación)

    Garantizar integridad de mensajes

    Prevenir ataques de intermediario (MITM)

2. Tipos de criptografía

    2.1 Criptografía simétrica

        Usa la misma clave para cifrar y descifrar.

        Rápida y eficiente para grandes volúmenes de datos.

        Ejemplos: AES, DES, RC4

    2.2 Criptografía asimétrica

        Usa un par de claves: pública y privada.

        Cifrado más lento, ideal para intercambio seguro de claves.

        Ejemplos: RSA, ECC

    2.3 Hashing

        No es cifrado.

        Transforma un mensaje en un valor fijo e irreversible.

        Se usa para verificar integridad (ej: SHA-256, MD5*)

        *Nota: MD5 y SHA1 ya no son seguros para criptografía moderna.

3. Protocolos criptográficos comunes

Protocolo       Uso principal                           Seguridad

SSL/TLS         Capa de cifrado en navegación web       TLS 1.2 o 1.3 seguro

SSH             Acceso remoto cifrado                   Robusto si se configura bien

IPsec           VPN entre sitios                        Segura, requiere buena configuración

PGP/GPG         Cifrado de correos y archivos           Muy seguro si se manejan bien las claves

4. Casos de uso en Blue Team

    Forzar HTTPS con TLS 1.2+ para proteger el tráfico web

    Cifrar discos duros con BitLocker o LUKS

    Configurar backups cifrados

    Verificar hashes de integridad de archivos descargados

    Detectar tráfico que evita cifrado (HTTP, FTP, Telnet)

    Configurar reglas en IDS/IPS para detectar cifrados anómalos

5. Buenas prácticas

    Usar cifrados fuertes: AES-256, RSA-2048 o superior

    Evitar algoritmos obsoletos: DES, RC4, MD5

    Rotar claves periódicamente

    Usar certificados válidos y actualizados

    Monitorear uso de criptografía débil en la red

6. Herramientas útiles para Blue Team

Herramienta             Uso principal

OpenSSL                 Generación y prueba de claves/certificados

GnuPG (GPG)             Cifrado y firma de archivos y correos

Hashdeep                Verificación de integridad con hashes

Wireshark               Análisis de protocolos cifrados

Nessus/OpenVAS          Detección de cifrados obsoletos en la red

7. Conceptos clave a dominar

    PKI (Infraestructura de Clave Pública)

    Certificados digitales y su validación

    Handshake TLS

    Cifrado en tránsito vs. en reposo

    Ataques comunes: downgrade, MITM, exfiltración con cifrado