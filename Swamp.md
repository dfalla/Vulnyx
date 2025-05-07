# Máquina Swamp

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.134

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,53,80 -vvv -Pn 192.168.5.134

![alt text](image-2.png)

### Fuzing web

feroxbuster --url http://192.168.5.134 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

![alt text](image-3.png)

agregamos el dominio al /etc/hosts

![alt text](image-4.png)

### Explotación

Como tenemos el servicio dns corriendo aplico el siguiente comado para buscar subdominios:

dig axfr @192.168.5.134 swamp.nyx

![alt text](image-5.png)

agregamos los subdominios al /etc/hosts

![alt text](image-6.png)

ahora hice fuzzing web a todos y el unico que encontré algo fue en: farfaraway.swamp.nyx

feroxbuster --url http://farfaraway.swamp.nyx/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

![alt text](image-7.png)

entre en el archivo.

![alt text](image-8.png)

copié el código en https://beautifier.io/ para verlo de una manera más limpia.

encontré lo siguiente:

![alt text](image-9.png)

lo desencripté con base64:

![alt text](image-10.png)

con esas credenciales entré por ssh

![alt text](image-11.png)


### Escalar privilegios

ejecuté sudo -l

![alt text](image-12.png)

### user.txt

![alt text](image-13.png)

### root.txt

![alt text](image-14.png)
