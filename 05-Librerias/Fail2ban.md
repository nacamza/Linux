## Fail2ban
Es una herramienta que nos da seguridad ante intentos de acceso al ssh por fuerza bruta
### Instalar en ubuntu
Primero agregamos el usuario, q vamos a utilizar para conectarnos, al grupo sudo 
````
sudo useradd MYUSER -G sudo
````
Despues, modifico las propiedades de los usuarios del grupo SUDO para que no pida contraseña  

Abrimos el archivo a modificar con el siguiente comando 
````
sudo visudo
````
Y agreagamos NOPASSWD:ALL, como se muestra a continuacion 
````
%sudo   ALL=(ALL:ALL) NOPASSWD:ALL
````
Configuramos para que las conecciones ssh soporten solo un usuario
````
sshd config AllowUsers USER
````
Inicio servico SSH
````
sudo systemctl enable ssh && sudo systemctl start ssh
````

## Instalamos fail2ban
```` 
apt-get install fail2ban
````
Abrimos el archivo de configuracion, buscamos **[sshd]** y lo configuramos para que despues de 3 intentos banee la ip por 86400 segundos
````
[sshd]

# To use more aggressive sshd modes set filter parameter "mode" in jail.local:
# normal (default), ddos, extra or aggressive (combines all).
# See "tests/files/logs/sshd" or "filter.d/sshd.conf" for usage example and details.
#mode   = normal
bantime = 86400
port    = ssh
logpath = %(sshd_log)s
backend = %(sshd_backend)s
maxretry = 3
````



