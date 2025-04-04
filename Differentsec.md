# Máquina Differentsec

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.145

![alt text](image-1.png)


### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 vvv -Pn 192.168.42.145

![alt text](image-2.png)

### Fuzzing web

gobuster dir -t 200 -u http://192.168.42.145/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git -b 403,404 2>/dev/null


![alt text](image-3.png)

### Explotación

Accedemos a la web:

![alt text](image-5.png)

y en la parte de abajo me da una opción para subir un archivo

![alt text](image-6.png)

Creamos un reverse shell llamado reverse.phtml con el código de pentestMonkey y lo subimos:


![alt text](image-4.png)


En Uploads:

![alt text](image-7.png)

nos ponemos en escucha 443 y le damos clic en reverse.phtml

![alt text](image-8.png)

hacemos tratamiento de la TTY


### Escalar privilegios

verificamos el /etc/crontab

![alt text](image-9.png)

se visualiza que el cronjob se ejecuta cada 1 min

verificamos los permisos:

![alt text](image-10.png)

entonces modificamos el archivo y colocamos el siguiente código:

![alt text](image-11.png)

nos ponemos en escucha con netcat:

![alt text](image-12.png)

### user.txt

![alt text](image-13.png)

### root.txt

![alt text](image-14.png)

