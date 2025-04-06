# Máquina Mux

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.156

![alt text](image-1.png)


### Servicios y versiones 

sudo nmap -sV --script vuln -p80,512,513,514 --min-rate 6000 -vvv 192.168.42.156

![alt text](image-2.png)

### Fuzzing web

gobuster dir -t 200 -u http://192.168.42.156/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git -b 403,404 2>/dev/null

![alt text](image-3.png)

entramos a la web y descargamos ls imagen de la Monna Lisa

![alt text](image-4.png)

aplicamos esteganografia, strings

![alt text](image-5.png)

![alt text](image-6.png)

Encontramos 2 contraseñas para el mismo usuario.

### Explotación

En el escaneo de servicios y versiones se puede ver que tiene activado el servicio exec con la version netkit-rsh rexecd que sirve para conexión remota.

rlogin 192.168.42.156 -l lisa

contraseña: Gi0c0nd@

![alt text](image-7.png)

### Escalar privilegios

![alt text](image-8.png)

ejecutamos:

![alt text](image-9.png)

![alt text](image-10.png)
### user.txt

![alt text](image-11.png)

### root.txt

![alt text](image-12.png)