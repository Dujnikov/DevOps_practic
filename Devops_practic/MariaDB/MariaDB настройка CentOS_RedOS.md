
Включаем в настройках vmware в сетевых настройка вместо nat - bridge. Запускаем машину.
В термиинале:
ip a - узнаем ip адрес машины
nano /etc/my.cnf.d/mariadb-server.cnf
раскоментировать строку bind-address=0.0.0.0
Сохранить конфиг
systemctl restart mariadb
mysql -u root -p
Вводим пароль
Затем
GRANT ALL PRIVILEGES ON aecatest.* TO 'aeca'@'%' IDENTIFIED BY 'aeca';

Вбиваем данные в Navicat ip машины, имя пользователя, пароль и порт 3306
Подключаемся и работаем.