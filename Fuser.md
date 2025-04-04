# Máquina Fuser

### Reconocimiento de la Ip de la máquina víctima

![alt text](image-8.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.146

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 vvv -Pn 192.168.42.146

![alt text](image-2.png)

### Explotación

Analizando CUPS el servicio que corre en el puerto 631:

![alt text](image-9.png)

La versión de CUPS tiene un exploit en github:

https://github.com/IppSec/evil-cups/blob/main/evilcups.py

copiamos el código de python y lo guardamos como epxloit.py

luego creamos un entorno virtual porque no me dejaba instalar un requerimiento.

![alt text](image-10.png)

nos ponemos en escucha con netcat en el puerto 443 y ejecutamos:

![alt text](image-4.png)

entramos en la url http://192.168.42.143:631 y en Printers observamos la ip de mi kali

![alt text](image-11.png)

le damos clic en la impresora que aparece la ip de mi kali

luego clic en Maintenance y en Print Test Page

![alt text](image-12.png)

y accedimos:

![alt text](image-13.png)

### Escalar privilegios

Ejectuamos find / -perm -4000 2>/dev/null para ver bit SUID

![alt text](image-14.png)

entonces ejecutamos:

/usr/bin/dash -p

![alt text](image-15.png)

### user.txt

![alt text](image-16.png)

### root.txt

![alt text](image-17.png)