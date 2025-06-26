# Máquina Observer
### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.169

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,111,135,139,445 -vvv -Pn 192.168.5.169



### Fuzzing Web

feroxbuster --url http://192.168.5.169/ -w /usr/share/seclists/Discovery/Web-Content/big.txt



### Explotación



### Escalar privilegios


### user.txt



### root.txt


