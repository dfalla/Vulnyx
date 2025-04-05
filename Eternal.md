# Máquina Eternal

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.152

![alt text](image-1.png)

### Servicios y versiones vulnerables

sudo nmap -sV --script vuln -p135,139,445 --min-rate 6000 -vvv 192.168.42.152

![alt text](image-2.png)

### Metasploit - Explotación

![alt text](image-3.png)

![alt text](image-4.png)

![alt text](image-5.png)

### user.txt

![alt text](image-6.png)

### root.txt

![alt text](image-7.png)