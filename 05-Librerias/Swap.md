## [Cómo ampliar la memoria SWAP en Linux](https://guidocutipa.blog.bo/como-ampliar-memoria-swap-linux/)
La SWAP es una zona del disco (un fichero o partición) que se usa para guardar las imágenes de los procesos que no han de mantenerse en memoria física.

## Verificar estado
El primer paso consiste en verificar la información del sistema con los siguientes comandos:
````
swapon –s
````
Con el comando free podemos verificar los distintos tipos de memoria:
````
free –m
````
El siguiente paso consiste en revisar el espacio disponible en las particiones del disco duro mediante el comando df:
````
df -h
````
## Configuración de un archivo SWAP
Crear el archivo SWAP de 4G con el comando fallocate:
````
fallocate -l 4G /swapfile
````
Comprobar que se ha creado el archivo
````
ls -lh /swapfile
````
Habilitar el archivo SWAP, primero es necesario ajustar los permisos de acceso:
````
chmod 600 /swapfile
````
El siguiente paso es notificar al sistema que el archivo se usará como memoria SWAP:
````
mkswap /swapfile
````
Activar el archivo como memoria SWAP
````
swapon /swapfile
````
Verificar que la nueva memoria SWAP esté configurada:
````
swapon -s
````
````
free -m
````
Hacer permanente los cambios en la memoria SWAP, modificando el archivo fstab:
````
nano /etc/fstab
````
Adicionar al final del archivo:
````
/swapfile   none    swap    sw    0   0
````
## Eliminar Swap
Ejecute el comando siguiente para desactivar el archivo swap
````
swapoff /swapfile
````
Elimine su entrada de /etc/fstab
Elimine el archivo actual
``
rm /swapfile
``
## Optimizar la Memoria SWAP
Para mejorar el rendimiento es necesario modificar el parámetro swappiness.
El «swappinness» es un valor que va de 0 a 100. Cuando el valor esté cerca de 0, no se intercambiará datos en el disco a menos que sea absolutamente necesario. Si por el contrario, el valor está más cerca de 100, se llevarán a cabo un mayor número de intercambios para dejar más espacio libre en la RAM.
````
nano /etc/sysctl.conf
````
Adicionar al final del archivo:
````
vm.swappiness=10
````
Reiniciar para aplicar los cambios
# [Instalar Zswap](https://geekland.eu/aligerar-el-sistema-con-zswap/) 
Zswap es un módulo del kernel de Linux desarrollado por Seth Jennings. Zswap se incorpora al Kernel de Linux a partir de la versión 3.11 y su principal función, al igual que Zram, es evitar la paginación en disco para de esta forma poder incrementar el rendimiento de nuestro sistema.

Verificar Kernel de Linux
````
uname -mrs
````
Abren una terminal y ejecutan el siguiente comando:
````
sudo nano /etc/default/grub
````
Una vez se abra el editor de texto tendremos que localizar una linea que empiece por el siguiente texto:
````
GRUB_CMDLINE_LINUX_DEFAULT
````
y modificarla con el siguiente valor
````
GRUB_CMDLINE_LINUX_DEFAULT="quiet zswap.enabled=1"
````
Una vez guardado el archivo tenemos que actualizar el grub para que se inicie Zswap en el próximo arranque de nuestro sistema operativo
````
sudo update-grub
````
Una vez actualizado el grub tan solo tenemos que reiniciar el ordenador. Una vez reiniciado el ordenador ya tan solo tenemos que comprobar que Zswap esté activado y funcionando
````
dmesg | grep zswap
````




