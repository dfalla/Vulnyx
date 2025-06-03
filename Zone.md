# Máquina Zone

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.159

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,53,80 -vvv -Pn 192.168.5.159

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.159/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)

vemos el robots.txt

![alt text](image-4.png)

colocamos el dominio en el /etc/hosts

como tenemos un dominio y el servicio dns activo ejecutamos:

dig axfr @192.168.5.159 securezone.nyx

![alt text](image-5.png)

agregamos los subdominios encontrados al /etc/hosts

accedimos a http://upl0ads.securezone.nyx/

![alt text](image-8.png)

### Explotación

pudimos subir un archivo rev.phar

luego me puse en escucha con netcat y pude acceder a la máquina

![alt text](image-6.png)

![alt text](image-7.png)

![alt text](image-9.png)

![alt text](image-10.png)

me conecto por ssh con el usuario hans con id_rsa encontrado

### Escalar privilegios

![alt text](image-11.png)

### user.txt

![alt text](image-12.png)

### root.txt

![alt text](image-13.png)