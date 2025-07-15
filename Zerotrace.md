# Máquina Zerotrace
### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.174

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.174

![alt text](image-2.png)


### Fuzzing Web
Realicé fuzzing web para descubrir directorios ocultos.

wfuzz -c -t 200 --hc=404 -w /usr/share/seclists/Discovery/Web-Content/big.txt "http://192.168.5.174/.FUZZ"

![alt text](image-3.png)

busqué archivos dentro del directorio oculto:

wfuzz -c --hc=404 -t 200 -w /usr/share/seclists/Discovery/Web-Content/big.txt  -z list,php-txt-md 'http://192.168.5.174/.admin/FUZZ.FUZ2Z'

![alt text](image-4.png)

como encontré un archivo php, busqué un parámetro para LFI

wfuzz -c --hl=0 -u "http://192.168.5.174/.admin/tool.php?FUZZ=/etc/passwd" -w /usr/share/wordlists/seclists/Discovery/Web-Content/burp-parameter-names.txt

![alt text](image-5.png)

verifiqué por la web

![alt text](image-6.png)

### Explotación

Busqué Procesos de línea de comandos

wfuzz -c -u "http://192.168.5.174/.admin/tool.php?file=/proc/FUZZ/cmdline" -z range,1-1000 --hw=0

![alt text](image-7.png)

analizo el proceso:

![alt text](image-8.png)

me conecté por ssh con las credenciales encontradas

![alt text](image-9.png)

ví archivos en los que tengo permisos de escritura:

![alt text](image-10.png)

no pude editar el archivo, entonces vi los permisos especiales, luego escribí una reverse shell en bash

![alt text](image-11.png)

me coloqué en escucha por el puerto 443 en mi kali:

![alt text](image-12.png)

volví a ejecutar el comando para ver en que archivos tengo permisos de escritura:

find / -writable 2>/dev/null | grep -v -i -E 'proc|sys|dev|run|irc|home|tmp'

![alt text](image-14.png)

verifico el archivo secret:

![alt text](image-15.png)

Este es un archivo de billetera (wallet) cifrada, típicamente utilizado en criptomonedas como Ethereum o otras redes basadas en blockchain. Este formato sigue el estándar JSON Wallet Key (versión 3)

entonces procedí a crackearla:

![alt text](image-16.png)

Ahora en el directorio del usuario ll104567 encontré un archivo llamado one con nombres de personajes:

![alt text](image-13.png)

a partir de este archivo creé uno anteponiendo la palabra dragonballz

![alt text](image-17.png)

ahora con la herramienta suForce procedí a encontrar la contraseña

![alt text](image-18.png)

cambié al usuario ll104567

![alt text](image-19.png)

### Escalar privilegios

![alt text](image-20.png)

### user.txt

![alt text](image-21.png)

### root.txt

![alt text](image-22.png)