### Общие команды

Что бы проверить статус сервера **MYSQL** выполните:

systemctl status mysql

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Что бы подключиться к серверу **MySQL** из консоли, если сервер **MySQL** находится на том же хосте:

mysql -u username -p

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Что бы подключиться к серверу **MySQL** из консоли, если сервер **MySQL** находится на удаленном хосте _db1.example.com_:

mysql -u username -p -h db1.example.com

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

### Работа с базами и таблицами

#### Работа с базами

Создать базу данных на **MySQL** сервере:

mysql> CREATE DATABASE [databasename];

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Показать список всех баз данных на сервере **MySQL**:

mysql> SHOW DATABASES;

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Переключиться для работы с определенной базой данных:

mysql> USE [db name];

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Удалить базу:

mysql> DROP DATABASE [database name];

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

#### Работа с таблицами

Отобразить все таблицы в базе данных:

mysql> SHOW TABLES;

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Просмотреть формат таблицы в базе:

mysql> DESCRIBE [table name];

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Показать все содержимое таблицы:

mysql> SELECT * FROM [table name];

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Отобразить количество строк в таблице:

mysql> SELECT COUNT(*) FROM [table name];

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Подсчитать количество колонок в таблице:

mysql> SELECT SUM(*) FROM [table name];

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Удаление строки в таблице:

mysql> DELETE from [table name] where [field name] = 'whatever';

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Удаление столбца из таблицы:

mysql> alter table [table name] DROP INDEX [column name];

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Удалить таблицу из базы:

mysql> DROP TABLE [table name];

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

##### Работа с колонками

Добавить колонку в таблицу:

mysql> ALTER TABLE [table name] ADD COLUMN [new column name] varchar (20);

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Изменение имени колонки:

mysql> ALTER TABLE [table name] CHANGE [old column name] [new column name] varchar (50);

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Создать колонку с уникальным именем, что бы избежать дубликатов в названиях:

mysql> ALTER TABLE [table name] ADD UNIQUE ([column name]);

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Изменение размера колонки:

mysql> ALTER TABLE [table name] MODIFY [column name] VARCHAR(3);

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

##### Выборка данных

Показать все содержимое таблицы:

mysql> SELECT * FROM [table name];

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Отобразить колонки и их содержимое в выбранной таблице:

mysql> SHOW COLUMNS FROM [table name];

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Отобразить строки в определенной  таблице, содержащие “_whatever_“:

mysql> SELECT * FROM [table name] WHERE [field name] = "whatever";

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Отобразить все записи в определенной таблице, содержащие “_Bob_” и телефонный номер “_3444444_:

mysql> SELECT * FROM [table name] WHERE name = "Bob" AND phone_number = '3444444';

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Отобразить все записи, **НЕ** содержащие имя “_Bob_” и телефонный номер “_3444444_“, отсортированные по полю _phone_number_:

mysql> SELECT * FROM [table name] WHERE name != "Bob" AND phone_number = '3444444' order by phone_number;

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Показать все записи, начинающиеся с букв ‘_bob_” и телефонного номера “_3444444_” в определенной таблице:

mysql> SELECT * FROM [table name] WHERE name like "Bob%" AND phone_number = '3444444';

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Показать все записи, начинающиеся с букв ‘_bob_” и телефонного номера “_3444444_“, ограничиваясь записями с 1-ой до 5-ой:

mysql> SELECT * FROM [table name] WHERE name like "Bob%" AND phone_number = '3444444' limit 1,5;

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Показать все уникальные записи:

mysql> SELECT DISTINCT [column name] FROM [table name];

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Отобразить выбранные записи, отсортированные по возрастанию (_asc_) или убыванию (_desc_):

mysql> SELECT [col1],[col2] FROM [table name] ORDER BY [col2] DESC;

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

##### Регулярные выражения

Использование регулярных выражений (_“REGEXP BINARY”_) для поиска записей. Например, для регистро-независимого поиска – найти все записи, начинающиеся с буквы _А_:

mysql> SELECT * FROM [table name] WHERE rec RLIKE "^a";

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

#### Импорт и экспорт данных в/из файла

Загрузка файла **CSV** в таблицу:

mysql> LOAD DATA INFILE '/tmp/filename.csv' replace INTO TABLE [table name] FIELDS TERMINATED BY ',' LINES TERMINATED BY 'n' (field1,field2,field3);

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

### Пользователи, пароли сервера **MySQL:**добавление, изменение пользователей и паролей

Создание нового пользователя – подключение к серверу **MySQL** под root, переключение к базе данных, добавление пользователя, обновление привилегий:

mysql -u root -p

mysql> USE mysql;

mysql> INSERT INTO user (Host,User,Password) VALUES('%','username', PASSWORD('password'));

mysql> flush privileges;

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Изменений пользовательского пароля из консоли на удаленном хосте _db1.example.org_:

mysqladmin -u username -h db1.example.org -p password 'new-password'

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Изменение пользовательского пароля из консоли **MySQL** – подключение под root, обновление пароля, обновление привилегий:

mysql> SET PASSWORD FOR 'user'@'hostname' = PASSWORD('passwordhere');

mysql> flush privileges;

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Восстановление/изменение пароля root сервера **MySQL** — остановка **MySQL**, запуск без таблиц привилегий, подключение под root, установка нового пароля, выход и перезапуск **MySQL**.

Подробнее о восстановлении пароля root для **MySQL** написано [тут>>>](http://rtfm.co.ua/mysql-smena-parolya-polzovatelya-root/ "MySQL: смена пароля пользователя root").

systemctl stop mysql

mysqld_safe --skip-grant-tables &

mysql -u root

mysql> use mysql;

mysql> update user set password=PASSWORD("newrootpassword") where User='root';

mysql> flush privileges;

mysql> quit

systemctl start mysql

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Обновление пароля root:

mysqladmin -u root -p oldpassword newpassword

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Установка права на подключение к серверу с хоста _localhost_ с паролем «_passwd_» — подключение под root, переключение к базе данных, установка привилегий, обновление привилегий:

mysql -u root -p

mysql> use mysql;

mysql> grant usage on *.* to bob@localhost identified by 'passwd';

mysql> flush privileges;

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Установка привилегий пользователю на использование базы данных — подключение под root, переключение к базе данных, установка привилегий, обновление привилегий:

mysql> use mysql;

mysql> INSERT INTO db (Host,Db,User,Select_priv,Insert_priv,Update_priv,Delete_priv,Create_priv,Drop_priv) VALUES ('%','databasename','username','Y','Y','Y','Y','Y','N');

mysql> flush privileges;

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Или:

mysql> grant all privileges on databasename.* to username@localhost;

mysql> flush privileges;

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Обновление информации в базе данных:

mysql> UPDATE [table name] SET Select_priv = 'Y',Insert_priv = 'Y',Update_priv = 'Y' where [field name] = 'user';

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Обновление привилегий в базе данных:

mysql> flush privileges;

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

### Резервные копии

#### Создание дампа

Создать резервную копию (dump) всех баз данных в файл _alldatabases.sql_:

mysqldump -u root -p password --opt >/tmp/alldatabases.sql

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Создать резервную копию одной базы данных в файл _databasename.sql_:

mysqldump -u username -p password --databases databasename >/tmp/databasename.sql

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Создать резервную копию одной таблицы в файл _databasename.tablename.sql_:

mysqldump -c -u username -p password databasename tablename > /tmp/databasename.tablename.sql

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

#### Восстановление из дампа

Восстановление базы данных (или таблицы) из резервной копии:

mysql -u username -p password databasename < /tmp/databasename.sql

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

### **Создание таблиц**

_курсивом_ указаны имена столбцов;  
ЗАГЛАВНЫМИ буквами – типы и атрибуты столцов;  
в (скобках) – значение типа столбца.

Создать таблицу, пример 1:

mysql> CREATE TABLE [table name] (firstname VARCHAR(20), middleinitial VARCHAR(3), lastname VARCHAR(35), suffix VARCHAR(3), officeid VARCHAR(10), userid VARCHAR(15), username VARCHAR(8), email VARCHAR(35), phone VARCHAR(25), groups VARCHAR(15), datestamp DATE, timestamp TIME, pgpemail VARCHAR(255));

-   Re-play
-   Copy to Clipboard
-   Pause
-   Full View

Создать таблицу, пример 2:

mysql> create table [table name] (personid INT(50) NOT NULL AUTO_INCREMENT PRIMARY KEY, firstname VARCHAR(35), middlename VARCHAR(50), lastname VARCHAR(50) default 'bato');