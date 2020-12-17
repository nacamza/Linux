### EnvSubst
El envsubst sustituye los valores de las variables de entorno. [Info](https://skofgar.ch/dev/2020/08/how-to-quickly-replace-environment-variables-in-a-file/)
### Configurar variables de entorno
````
export SERVER_URL=https://gitlab.com/skofgar
export USER_NAME=foo_user
export USER_PASSWORD=mymonkey
````
o podemos guardarlas en un archivo (por ejemplo .env) y luego cárguelos en su sesión de shell actual usando ``source .env``
Si queremos modificar el actual
````
envsubst < config.txt
````
### Sustitución
Si queremos crear un nuevo archivo
````
envsubst < "source.txt" > "destination.txt"
````
## Ejemplo
Creamos los archivos **source.txt** y **.env**
#### Source.txt
````
Url = ${SERVER_URL}
User = ${USER_NAME}
Pass = ${USER_PASSWORD}
````
#### .env
````
export SERVER_URL=https://gitlab.com/skofgar
export USER_NAME=foo_user
export USER_PASSWORD=mymonkey
````
Luego levantamos las variables de entorno
````
source .env
````
y luego ejecutamos 
````
envsubst < "source.txt" > "destination.txt"
````

[Mas info](https://github.com/a8m/envsubst)
