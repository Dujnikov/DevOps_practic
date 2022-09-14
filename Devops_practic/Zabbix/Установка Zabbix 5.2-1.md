# wget https://repo.zabbix.com/zabbix/5.2/ubuntu/pool/main/z/zabbix-release/zabbix-release_5.2-1%2Bubuntu20.04_all.deb
# sudo  dpkg -i zabbix-release_5.2-1+ubuntu20.04_all.deb
# apt update


 Установим Zabbix сервер, веб-интерфейс и агент
#  sudo apt install mysql-server zabbix-frontend-php zabbix-apache-conf zabbix-agent


Создайте базу данных

#  sudo mysql -u root -p 
password
mysql create database zabbix character set utf8 collate utf8_bin;
mysql create user zabbix@localhost identified by 'password';
mysql grant all privileges on zabbix.* to zabbix@localhost;
mysql quit;

Установим zabbix-server-mysql 
# sudo apt install zabbix-server-mysql

Импортируем настройки.
# zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -uzabbix -p zabbix


Отредактируйте файл /etc/zabbix/zabbix_server.conf

DBPassword=password


Запустите процессы Zabbix сервера и агента
Запустите процессы Zabbix сервера и агента и настройте их запуск при загрузке ОС.

# systemctl restart zabbix-server zabbix-agent apache2
# systemctl enable zabbix-server zabbix-agent apache2

Доступ в веб интерфейс.
Admin  zabbix

Установка агента Zabbix

# wget https://repo.zabbix.com/zabbix/5.2/ubuntu/pool/main/z/zabbix-release/zabbix-release_5.2-1%2Bubuntu20.04_all.deb
# sudo  dpkg -i zabbix-release_5.2-1+ubuntu20.04_all.deb
# apt update

#  sudo apt install  zabbix-agent

#  sudo nano /etc/zabbix/zabbix_agentd.conf

https://www.youtube.com/watch?v=-DdDnmAAlgk
