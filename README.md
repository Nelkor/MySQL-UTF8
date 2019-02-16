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

### Очистить таблицу, привязанную к другой таблице

SET FOREIGN_KEY_CHECKS = 0;  
TRUNCATE table $table_name;  
SET FOREIGN_KEY_CHECKS = 1;  

### Оптимизируем OFFSET LIMIT

/* не оптимизированно */  
SELECT u.first_name, c.name FROM users as u LEFT JOIN cities as c ON u.cityId = c.id LIMIT 999000, 10;  

/* оптимизированно */  
SELECT u.first_name, c.name FROM users as u LEFT JOIN cities as c ON u.cityId = c.id JOIN (SELECT id FROM users ORDER BY id LIMIT 999000, 10) as t ON t.id = u.id;  
