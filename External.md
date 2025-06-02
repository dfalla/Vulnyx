# Máquina External

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.157

![alt text](image-1.png)


### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80,3306 -vvv -Pn 192.168.5.157

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.157/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

No encontré nada interesante.

hice curl a http://192.168.5.157/

y visualicé:

![alt text](image-3.png)

lo agregué al /etc/hosts:

![alt text](image-4.png)

busco subdominios:

![alt text](image-5.png)

agrego al /etc/hosts

![alt text](image-6.png)

voy a la web y encuentro:

![alt text](image-7.png)

pruebo credenciales y me sale:

![alt text](image-8.png)


### Explotación 

intercepto con burp suite:

![alt text](image-9.png)

estoy ante un XXE:  https://book.hacktricks.wiki/en/pentesting-web/xxe-xee-xml-external-entity.html

creo un archivo vuln con el siguiente código:

![alt text](image-10.png)

ejecuto:

curl -X POST "http://administrator.ext.nyx/form.php" --upload-file "vuln"

![alt text](image-11.png)

cambiamos la ruta para ver archivos:

![alt text](image-12.png)

![alt text](image-13.png)

entré a mysql:

![alt text](image-15.png)

![alt text](image-14.png)

### Escalar privilegios

![alt text](image-16.png)

### user.txt

![alt text](image-17.png)

### root.txt

![alt text](image-18.png)