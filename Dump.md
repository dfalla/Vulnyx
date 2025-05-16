# Máquina Dump

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.145

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p21,80,4200 -vvv -Pn 192.168.5.145

![alt text](image-2.png)

![alt text](image-3.png)


### Fuzing web

feroxbuster --url http://192.168.5.145/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

No encontramos nada

![alt text](image-6.png)

### Ftp

Iniciamos sesión con anonymous, etramos en .backup y luego descargamos sam.bak system.bak

![alt text](image-4.png)

![alt text](image-5.png)

### Explotación

![alt text](image-7.png)

entramos en https://192.168.5.145:4200/

iniciamos sesión con el usuario dumper y la contraseña 1dumper

![alt text](image-8.png)

ejecuté una bash para conectarme por netcat:

![alt text](image-10.png)

luego me di cuenta que puedo ver el archivo shadow:

![alt text](image-11.png)

crackié la contraseña

![alt text](image-9.png)

### Escalar privilegios

ejecuté ss -tuln

![alt text](image-12.png)

usé chisel para el port forwarding

en la máquina víctima

![alt text](image-13.png)

en kali:

![alt text](image-14.png)

ahora me conecto por ssh con las credenciales de root

![alt text](image-15.png)

### user.txt

![alt text](image-16.png)

### root.txt

![alt text](image-17.png)