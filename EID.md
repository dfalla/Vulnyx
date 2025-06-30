# Máquina EID
### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.171

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.171

![alt text](image-2.png)

agrego el dominio al /etc/hosts

![alt text](image-3.png)

### Fuzzing Web

feroxbuster --url http://192.168.5.171/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-4.png)

busqué subdominios:

wfuzz -H "Host: FUZZ.3id.nyx" -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u http://3id.nyx --hw=12

![alt text](image-5.png)

### Explotación

Hago fuerza bruta al formulario de login

![alt text](image-6.png)

luego veo el siguiente mensaje

![alt text](image-7.png)

pruebo SSTI:

![alt text](image-8.png)

utilizo un código en python para entrar en la máquina

![alt text](image-9.png)

Para cambiar al usuario alouch, hago el siguiente artificio

![alt text](image-10.png)

copio el 3id_key.pub

![alt text](image-11.png)

lo reemplazo en la máquina objetivo

![alt text](image-12.png)

me conecto por ssh con el usuario alouch

![alt text](image-13.png)

### Escalar privilegios

![alt text](image-14.png)

ejecutamos:

sudo /opt/eid_scripts/maintenance_cleanup.sh /etc/passwd

estando dentro de less

!/bin/bash

![alt text](image-15.png)

### user.txt

![alt text](image-16.png)

### root.txt

![alt text](image-17.png)