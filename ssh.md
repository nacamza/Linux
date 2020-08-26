# Coneccion ssh
## Generar claves publica y privada
````
ssh-keygen
````
Para ver la clave publica 
````
cat .ssh/id_rsa.pub
````
Y la privada
````
cat .ssh/id_rsa
````
## Ahora tenemos que copiar la clave publica en el server destino en authorized_keys
````
nano .ssh/authorized_keys
````
En el archiva copiamos la clave publica

## Ahora podemos ingresar al server
````
ssh user@ip
````
