# MySQL-UTF8

apt-get install mysql-server

### После установки создадим файл:

vim /etc/mysql/conf.d/utf8_set.cnf

### Добавим в файл:

[mysqld]  
init_connect='SET collation_connection = utf8mb4_unicode_ci'  
character-set-server = utf8mb4  
collation-server = utf8mb4_unicode_ci  

[client]  
default-character-set = utf8mb4  

### Перезапустим сервис mysql:

service mysql restart

### Создать пользователя + настройка прав

CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';  
GRANT ALL PRIVILEGES ON database.* TO 'newuser'@'localhost';  
