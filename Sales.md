# Máquina Sales
### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.170

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.170

![alt text](image-2.png)

agregué el dominio al /etc/hosts

![alt text](image-3.png)

### Fuzzing Web

feroxbuster --url http://192.168.5.170/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

No encontré nada interesante

entré a la web y encontré un usuario

![alt text](image-4.png)

busqué subdominios

wfuzz -H "Host: FUZZ.sales.nyx" -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u http://sales.nyx --hw 28

![alt text](image-5.png)

lo agregué al /etc/hosts

![alt text](image-6.png)

enumeré el subdominio

feroxbuster --url http://crm.sales.nyx/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-7.png)

entramos en la url encontrada 

![alt text](image-8.png)

Creo una lista de contraseñas:

![alt text](image-9.png)

intercepto la petición del inicio de sesión

![alt text](image-10.png)

En la web sales.nyx encontré usuarios y los agregué a un archivo users.txt

ejecuté el comando:

ffuf -r -fs 11571 -w passwords.txt:FUZZPASS -w users.txt:FUZZUSER -u "http://crm.sales.nyx/index.php" -d "module=Users&action=Authenticate&return_module=Users&return_action=Login&cant_login=&login_module=&login_action=&login_record=&login_token=&login_oauth_token=&login_mobile=&user_name=FUZZUSER&username_password=FUZZPASS&Login=Log+In" -H "Content-Type: application/x-www-form-urlencoded"

![alt text](image-11.png)

busco algún archivo que me dé la versión

wfuzz -c --hc=404 -t 200 -w /usr/share/seclists/Discovery/Web-Content/big.txt  -z list,php-txt-md 'http://crm.sales.nyx/FUZZ.FUZ2Z'

![alt text](image-13.png)

accedo por la web

![alt text](image-12.png)


### Explotación

Encontré un exploit para la versión

![alt text](image-14.png)

![alt text](image-15.png)

![alt text](image-16.png)

![alt text](image-17.png)

eumero usuarios:

![alt text](image-18.png)

visualizo el archivo config.php

![alt text](image-19.png)

![alt text](image-20.png)

cambio al usuario eve

### Escalar privilegios

siendo el usuario eve:

![alt text](image-21.png)

en /tmp creo el archivo pe.c

![alt text](image-22.png)

![alt text](image-23.png)

### user.txt

![alt text](image-24.png)

### root.txt

![alt text](image-25.png)