# Máquina Share

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.161

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sV --script vuln -p22,80,8080 --min-rate 6000 -vvv 192.168.42.161

![alt text](image-2.png)

### Entramos en la web

http://192.168.42.161:8080/

![alt text](image-3.png)



### Explotación

verificamos en exploit-db

https://www.exploit-db.com/exploits/14925

entonces tenemos un caso de LFI

![alt text](image-4.png)

verifico el id_rsa de tim

![alt text](image-5.png)

sacamos el hash del id_rsa

![alt text](image-6.png)

crackeamos el hash con johntheripper

![alt text](image-7.png)

![alt text](image-8.png)

![alt text](image-9.png)

### Escalar privilegios

![alt text](image-10.png)

### user.txt

![alt text](image-11.png)

### root.txt

![alt text](image-12.png)