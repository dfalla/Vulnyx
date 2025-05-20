# Máquina Load

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.148

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.148

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.148/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)

al parecer hay una ruta /ritedev/, vamos a verificar el robots.txt

![alt text](image-4.png)

se confirma en el robots que existe esa ruta.

Entramos en la ruta:

![alt text](image-5.png)

se verifica que es RiteCMS en la versión 3.0


### Explotación

Seguimos estos pasos para entrar en la máquina

La vulnerabilidad pertence a RITECMS 3.1.0

- Nos dirijimos http://192.168.5.148/ritedev/admin.php

- Nos autenticamos, admin: admin 

- Clic en Admin

- luego clic en files manager

- eliminamos el .htaccess en el directory media y en file

- subimos un reverseshell en php

- Nos ponemos en escucha con netcat por el puerto del reverse shell

- accedmos a  http://192.168.5.148/ritedev/files/rev.php

- Listo estamos dentro

![alt text](image-6.png)

ejecutamos en la url:

![alt text](image-7.png)

con netcat

![alt text](image-8.png)

Vemos los usuarios del sistema:

![alt text](image-9.png)

ejecuto sudo -l

![alt text](image-10.png)

Cambiamos al usuario travis:

![alt text](image-11.png)

al ejecutar el comando sudo -u travis /usr/bin/crash -h

se nos abre una ventana y escribimos:

!sh

### Escalar privilegios

![alt text](image-12.png)

![alt text](image-13.png)

copiamos el id_rsa, le damos permisos 600 y ejceutamos:

![alt text](image-14.png)

### user.txt

![alt text](image-15.png)

### root.txt

![alt text](image-16.png)