# Máquina Lower4

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.139

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,113 vvv -Pn 192.168.42.139

![alt text](image-2.png)


### Explotación

El servicio ident es un servicio de identificación de usuarios, por lo tanto lucifer es un usuario que ha hecho conexión con el sistema.

Ataqu de fuerza bruta:

hydra -l lucifer -P /usr/share/wordlists/rockyou.txt 192.168.42.139 ssh

![alt text](image-3.png)

nos conectamos por ssh

![alt text](image-4.png)

### user.txt

![alt text](image-6.png)

### Escalar privilegios

sudo -l

![alt text](image-5.png)

![alt text](image-7.png)

### root.txt

![alt text](image-8.png)