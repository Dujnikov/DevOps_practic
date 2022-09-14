dnf update
dnf install mariadb-server
mariadb -V
systemctl enable mariadb
systemctl start mariadb
systemctl status mariadb
sudo nano /etc/selinux/config - disabled 
sudo reboot
mysql -u root -p
CREATE DATABASE aecatest CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
GRANT ALL PRIVILEGES ON aecatest.* TO 'aeca'@'localhost' IDENTIFIED BY 'aeca';
Далее производится установка aeca пакета
 yum install ./aeca-1.0.0-97.x86_64.rpm
 ./install.sh - скрипт установки