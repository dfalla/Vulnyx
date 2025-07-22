# Máquina Bola
### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.175

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,873 -vvv -Pn 192.168.5.175

![alt text](image-2.png)

Agregamos al /etc/hosts el dominio


### Fuzzing Web

dirsearch -u http://bola.nyx

![alt text](image-3.png)

entramos por la web:

![alt text](image-7.png)

![alt text](image-8.png)

![alt text](image-4.png)

![alt text](image-5.png)

Encuentré la carpeta extensions y la descargué en mi kali

![alt text](image-6.png)

siguiendo los pasos de: Password_manager_FirefoxExtension-VulNyx.pdf

![alt text](image-9.png)

![alt text](image-10.png)

Inicié sesión en el login encontrado anteriormente:

![alt text](image-11.png)

nombrar los archivo como un hash md5, entonces descubrí que era el nombre de usuario de jackie0x17 pero en md5, entonces verifiqué la url para descargar el archivo y probé generando un hash md5 para los otros usuarios encontrados.

http://bola.nyx/download.php?file_name=115a2cf084dd7e70a91187f799a7d5a8.pdf

generé el hash md5 con d4t4s3c

![alt text](image-12.png)

lo descargué:

http://bola.nyx/download.php?file_name=97035ded598faa2ce8ff63f7f9dd3b70.pdf

al abrirlo me encontré con las credenciales de admin y una url

![alt text](image-13.png)

![alt text](image-14.png)


### Explotación

Hice port fordwarding con ssh utilizando las credenciales d4t4s3 y la contraseña: VulNyxtestinglogin123

![alt text](image-15.png)

visualizo el servidor wsdl por el puerto 9000:

![alt text](image-16.png)

![alt text](image-17.png)

Intercepté la petición con burp suite y lo mandé al repetidor, cambié la petición a POST

![alt text](image-18.png)

![alt text](image-19.png)

Cambié ExecuteCommand por LoginRequest

![alt text](image-20.png)

envié una reverse shell

### Escalar privilegios


### user.txt



### root.txt

