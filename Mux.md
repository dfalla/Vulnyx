# Máquina Mux

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.156

![alt text](image-1.png)


### Servicios y versiones 

sudo nmap -sV --script vuln -p80,512,513,514 --min-rate 6000 -vvv 192.168.42.155



### Fuzzing web

gobuster dir -t 200 -u http://192.168.42.155/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git -b 403,404 2>/dev/null


### Explotación



### Escalar privilegios



### user.txt



### root.txt

