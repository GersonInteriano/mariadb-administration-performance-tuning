# mariadb-administration-performance-tuning
Despliegue securizado, optimización de rendimiento (Performance Tuning) y automatización de planes de contingencia (Backup/Restore) en MariaDB sobre entornos Linux Linux (Debian/Ubuntu).

Este proyecto documenta el ciclo completo de despliegue, securización, auditoría de rendimiento y alta disponibilidad de un Sistema Gestor de Bases de Datos Relacionales (SGBD) **MariaDB/MySQL** sobre una infraestructura virtualizada Linux (Debian/Ubuntu). 

El escenario se basa en **barbacoa-asix**, una base de datos diseñada para la gestión logística, de pagos y control de suministros de eventos.

---

---

Apartat 1.1 – Instal·lació i configuració inicial
Instal·la MariaDB o MySQL en una màquina virtual Linux (Debian/Ubuntu), o  una màquina en la que previament estigui instal·lat Mysql.
Se aplica el comando sudo apt update para la actualización de los paquetes:



Es localitza el fitxer de configuració principal (/etc/mysql/mariadb.conf.d/50-server.cnf o equivalent) i es modifica els paràmetres següents:
max_connections = 50
innodb_buffer_pool_size = 40% de la RAM disponible a la MV
bind-address = 127.0.0.1 (accés local) → canvia-ho posteriorment per permetre accés des de la IP del company.
character-set-server = utf8mb4
Es reinicia el servei i es procedeix a comprovar que els canvis s'han aplicat amb SHOW VARIABLES LIKE 'max_connections' i SHOW VARIABLES LIKE 'innodb_buffer_pool_size'.


