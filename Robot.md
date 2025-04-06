# Máquina Robot

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.158

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sV --script vuln -p22,80,27017 --min-rate 6000 -vvv 192.168.42.158

![alt text](image-2.png)

![alt text](image-3.png)



### Fuzzing web

gobuster dir -t 200 -u http://192.168.42.158/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git -b 403,404 2>/dev/null

![alt text](image-4.png)

entramos a index.html

![alt text](image-5.png)

Descargamos la imagen:

![alt text](image-6.png)

aplicamos esteganografia con exiftool:

![alt text](image-7.png)

aplicamos gobuster otra vez:

gobuster dir -t 200 -u http://192.168.42.158/B4ckUp_3LLi0t/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git -b 403,404 2>/dev/null

![alt text](image-8.png)

visualisamos lo que contiene connect.bak

![alt text](image-9.png)

me conecto a mongodb con las credenciales encontradas hacia la base de dato elliot

![alt text](image-10.png)

![alt text](image-11.png)


### Explotación

Usé la herramienta cupp para crear un diccionario de contraseñas con la información encontrada en mongodb

![alt text](image-12.png)

![alt text](image-13.png)

### Escalar privilegios

![alt text](image-14.png)

![alt text](image-15.png)

### user.txt

![alt text](image-16.png)

### root.txt

![alt text](image-17.png)