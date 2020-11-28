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
