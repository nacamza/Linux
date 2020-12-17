## [Crontab](https://www.hostinger.com.ar/tutoriales/cron-job/)
Cron es una herramienta que se utiliza en GNU/Linux y Unix, y que sirve para programar la ejecución de comandos o scripts en el sistema, en base a una fecha y hora específicas. Cron permanece siempre activo y en segundo planto.

Lo primero sería visualizar el contenido de ese fichero en tu sistema.
````
sudo crontab -l
````
El siguiente paso, por tanto, es rellenar el fichero con la tarea que quieres que se ejecute de forma automática
````
sudo crontab -e
````
Lo siguiente que verás es la interfaz del editor Nano por pantalla, y ya solo queda empezar a editar el fichero.Para ello, debes especificar cada tarea a ejecutar en una linea aparte, y siguiendo el siguiente formato:
````
* * * * * orden-ejecución
````
![](https://www.hostinger.es/tutoriales/wp-content/uploads/sites/7/2020/05/a-crontab-file-consist-of-five-fields-768x110.png)

Los asteriscos van separados por un espacio y sirven para indicar el contexto de ejecución. Puedes sustituir cada uno de ellos con el valor correspondiente en cada uno de estos casos:
- Minuto. Indicar un valor de 0 a 59.
- Hora. Indicar un valor de 0 a 23.
- Día del més. Indicar un valor de 1 a 31.
- Mes. Indicar un valor de 1 a 12.
- Día de la semana. Indicar un valor de 0 (domingo) a 6 (sábado).

Además de eso, debes usar los caracteres adecuados en cada archivo crontab.

- Asterisco (*): para definir todos los parámetros de programación.
- Coma (,): para mantener dos o más tiempos de ejecución de un solo comando.
- Guión (-): para determinar el intervalo de tiempo al configurar varios tiempos de ejecución de un solo comando.
- Barra oblicua (/): para crear intervalos de tiempo predeterminados en un rango específico.
- Último (L): para el propósito específico de determinar el último día de la semana en un mes determinado. Por ejemplo, 3L significa el último miércoles.
- Día de la semana (W): para determinar el día de la semana más cercano de un momento determinado. Por ejemplo, 1W significa que si el 1 de un mes es un sábado, el comando se ejecutará el lunes (el 3 del mes).
- Hash (#): para determinar el día de la semana, seguido de un número que va del 1 al 5. Por ejemplo, 1#2 significa el segundo lunes
- Signo de interrogación (?): para dejar en blanco.

Otra opción para indicar el contexto de ejecución es sustituir todos los asteriscos por una sola palabra reservada
````
@reboot sudo sh /home/nahuel/init.sh
````
````
@reboot sleep 300 && sudo sh /home/nahuel/init.sh
````
Ejemplo init.sh
````
sleep 30
cd /home/nahuel/Deploy
sudo docker-compose up -d
````
Crontab por defecto guarda logs en
````
/var/log/syslog
````
Para ver los logs de Crontab
````
grep CRON /var/log/syslog
````
Con esto ya tienes el fichero crontab configurado para ejecutar el script en cada arranque del sistema. Queda la tarea de comprobar que el servicio asociado a Cron esté habilitado. 
````
sudo systemctl status cron.service
````
Lo más habitual es que te indique que el servicio está activo. Si por lo que fuera, te indicase lo contrario, puedes habilitarlo con el siguiente comando:
````
sudo systemctl enable cron.service
````



