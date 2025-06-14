# Máquina Blog

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.162



### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.162



### Fuzzing web

feroxbuster --url http://192.168.5.162/ -w /usr/share/seclists/Discovery/Web-Content/big.txt


### Explotación



### Escalar privilegios



### user.txt



### root.txt
