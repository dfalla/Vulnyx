# Máquina Lower2

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.140

![alt text](image-1.png)


### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,23,80 vvv -Pn 192.168.42.140

![alt text](image-2.png)


### Explotación

Intenté iniciar sesión por ssh y al fracasar me salió un usuario.

![alt text](image-3.png)

hice un ataque de fuerza bruta a telnet.

hydra -l b.taylor -P /usr/share/wordlists/rockyou.txt 192.168.42.140 telnet

![alt text](image-4.png)

inicié sesión por telnet

![alt text](image-5.png)



### user.txt

![alt text](image-9.png)

### Escalar privilegios

ejecutamos el comando id:

![alt text](image-7.png)

Entonces veo que pertenezco al grupo shadow, por lo tanto puedo editar el archivo /etc/shadow

![alt text](image-8.png)

eliminamos el hash de la contraseña de root

![alt text](image-6.png)

su root y no escribimos contraseña:

![alt text](image-10.png)

### root.txt

![alt text](image-11.png)