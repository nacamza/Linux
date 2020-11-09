## Fail2ban
Es una herramienta que nos da seguridad ante intentos de acceso al ssh por fuerza bruta

https://www.linode.com/docs/guides/using-fail2ban-to-secure-your-server-a-tutorial/

## Instalamos fail2ban
```` 
apt-get install fail2ban
````
Abrimos el archivo de configuracion
````
sudo nano /etc/fail2ban/jail.conf
````
Buscamos **[sshd]** y lo configuramos para que despues de 3 intentos banee la ip por 86400 segundos
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
Iniciamos el servicio
````
systemctl start fail2ban
````
Y habilitamos el servicio
````
systemctl enable fail2ban
````
Para ver los logs de fail2ban
````
sudo nano /var/log/fail2ban.log
````

### Aceptar solo un usuario por ssh
https://eltallerdelbit.com/permisos-usuarios-grupos-ssh-server/
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


