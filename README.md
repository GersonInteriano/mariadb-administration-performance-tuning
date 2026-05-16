# mariadb-administration-performance-tuning
Despliegue securizado, optimización de rendimiento (Performance Tuning) y automatización de planes de contingencia (Backup/Restore) en MariaDB sobre entornos Linux Linux (Debian/Ubuntu).

Este proyecto documenta el ciclo completo de despliegue, securización, auditoría de rendimiento y alta disponibilidad de un Sistema Gestor de Bases de Datos Relacionales (SGBD) **MariaDB/MySQL** sobre una infraestructura virtualizada Linux (Debian/Ubuntu). 

El escenario se basa en **barbacoa-asix**, una base de datos diseñada para la gestión logística, de pagos y control de suministros de eventos.

---

---

Apartado 1.1 – Instalación y configuración inicial
Instala MariaDB o MySQL en una máquina virtual Linux (Debian/*Ubuntu), o una máquina en la que previament esté instalado Mysql.

Se aplica el comando sudo apt update para la actualización de los paquetes:

<img width="891" height="423" alt="image" src="https://github.com/user-attachments/assets/cba6dbec-ed6e-4d94-bf6b-c16274a11f05" />

Seguidamente se procede a instalar el servicio. Para este caso se utilizará MariaDB

<img width="970" height="353" alt="image" src="https://github.com/user-attachments/assets/4f482792-1383-4663-8d22-cc0fc7852659" />

Se revisa el estado del sevicio.

<img width="860" height="296" alt="image" src="https://github.com/user-attachments/assets/329c2ad0-0b8d-4f10-8548-bef50c1d974b" />


Se localiza el fichero de configuración principal (/etc/mysql/*mariadb.conf.d/50-server.cnf o equivalente) y se modifica los parámetros siguientes:



Se utiliza un editor para la modificación de las variables, en este case se hace uso de nano

<img width="1025" height="42" alt="image" src="https://github.com/user-attachments/assets/9fce96a9-085c-45f7-b1fc-aaabdcc598e2" />

Se modifica la variable max_connections a 50 y la bind-address a la ip del servidor para que el servicio MariaDB pueda escuchar conexiones desde esa red especifica.

<img width="696" height="388" alt="image" src="https://github.com/user-attachments/assets/5c9d6e0a-645e-4b4b-b339-4ecb2102e940" />

Se modifica la variable character-set-server a utf8mb4 y innodb_buffer_pool_size al 40% de la memoria RAM disponible, quedando con un total de 1638 megabytes de 8 gigabytes.

<img width="589" height="339" alt="image" src="https://github.com/user-attachments/assets/6ca8c3a1-31b1-4b5f-99cc-81d1113a22aa" />

Se reinicia el servicio y se procede a comprobar que los cambios se han aplicado con SHOW VARIABLES LIKE 'max_connections' y SHOW VARIABLES LIKE 'innodb_buffer_pool_size'.

<img width="933" height="633" alt="image" src="https://github.com/user-attachments/assets/54c6055c-ae5d-4e93-9e91-d2bf0275fa20" />



Procedimiento para recuperar la contraseña en caso de olvido:

Se detiene el servicio y se aplica el comando para el modo recuperación

<img width="1157" height="123" alt="image" src="https://github.com/user-attachments/assets/914e24b6-b920-4487-abeb-7430fb5bdfd8" />

Se entra al servicio con usuario root.

<img width="813" height="204" alt="image" src="https://github.com/user-attachments/assets/1ad92143-0c5e-4f41-84ab-98c85fc0b167" />

Se recargan los privilegios y se cambia la contraseña del usuario root:

<img width="787" height="265" alt="image" src="https://github.com/user-attachments/assets/efe09728-c67b-45de-aed0-efc1f7e232e7" />

Se termina el servicio de mysql y se termina el proceso en segundo plano del modo reccuperación para iniciar nuevamente el servicio.

<img width="1008" height="116" alt="image" src="https://github.com/user-attachments/assets/e596b60f-5dbf-4f5b-85dd-f70ea8703e01" />

Una vez hecho este procedimiento el servicio se puede utilizar con normalidad.
