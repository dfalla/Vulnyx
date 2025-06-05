# Máquina Ready

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.161

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,6379,8080 -vvv -Pn 192.168.5.161

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.161/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

No se encontró nada importante

feroxbuster --url http://192.168.5.161:8080/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

Tampoco se encontró nada importante

### Explotación

hacemos una configuración en redis:

![alt text](image-3.png)

ejecuto rev.php por url:

![alt text](image-4.png)

me puse en escucha con netcat por el puerto 443

![alt text](image-5.png)

vi los usuarios:

![alt text](image-6.png)

### Escalar privilegios

![alt text](image-7.png)

ejecuté

![alt text](image-8.png)

copié el id_rsa y lo pasé por RSAcrack para ver el passprhase

![alt text](image-9.png)

me conecté por ssh con el usuario root

![alt text](image-10.png)

### user.txt

![alt text](image-11.png)

### root.txt

![alt text](image-12.png)

![alt text](image-13.png)