### EnvSubst
El envsubst sustituye los valores de las variables de entorno. [Info](https://skofgar.ch/dev/2020/08/how-to-quickly-replace-environment-variables-in-a-file/)
### Configurar variables de entorno
````
export SERVER_URL=https://gitlab.com/skofgar
export USER_NAME=foo_user
export USER_PASSWORD=mymonkey
````
o podemos guardarlas en un archivo (por ejemplo .env) y luego cárguelos en su sesión de shell actual usando ``source .env``
### Sustitución
Si queremos crear un nuevo archivo
````
envsubst < "source.txt" > "destination.txt"
````
Si queremos modificar el actual
````
envsubst < config.txt
````
[Mas info](https://github.com/a8m/envsubst)
