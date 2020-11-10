## Fail2ban
Es una herramienta que nos da seguridad ante intentos de acceso por fuerza bruta

https://www.linode.com/docs/guides/using-fail2ban-to-secure-your-server-a-tutorial/

## Instalamos fail2ban
```` 
apt-get install fail2ban
````
Abrimos el archivo de configuración
````
sudo nano /etc/fail2ban/jail.conf
````
Podemos modificar las reglas generales donde:
- bantime: es el tiempo de baneo
- findtime: es la ventana de tiempo donde se cuentan los intentos fallidos
- maxretry: cantidad máxima de intentos 
````
# External command that will take an tagged arguments to ignore, e.g. <ip>,
# and return true if the IP is to be ignored. False otherwise.
#
# ignorecommand = /path/to/command <ip>
ignorecommand =

# "bantime" is the number of seconds that a host is banned.
bantime  = 10m

# A host is banned if it has generated "maxretry" during the last "findtime"
# seconds.
findtime  = 10m

# "maxretry" is the number of failures before a host get banned.
maxretry = 5
````
O buscar un servicio en particular, buscamos **[sshd]** para configurar el acceso por ssh y lo configuramos para que después de 3 intentos banee la ip por 86400 segundos
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
service start fail2ban
````
Para ver los logs de fail2ban
````
sudo nano /var/log/fail2ban.log
````

### Aceptar solo un usuario por ssh 
https://eltallerdelbit.com/permisos-usuarios-grupos-ssh-server/

Generamos el usuario si no existe
````
sudo adduser MyUser
````
Agregamos el usuario, q vamos a utilizar para conectarnos, al grupo sudo 
````
usermod -a -G sudo MyUser
````
Despues, modifico las propiedades de los usuarios del grupo SUDO para que no pida contraseña  

Abrimos sudoers con el siguiente comando (verifica sintaxis) 
````
sudo visudo
````
Y agregamos NOPASSWD:ALL, como se muestra a continuación 
````
%sudo   ALL=(ALL:ALL) NOPASSWD:ALL
````
Abrimos el archivo de configuración ssh
````
nano /etc/ssh/sshd_config
````
Configuramos para que las conexiones ssh soporten solo un usuario, agregamos la siguiente línea al final del archivo
````
AllowUsers MyUser
````
Inicio servicio SSH
````
sudo systemctl enable ssh && sudo systemctl start ssh
````

