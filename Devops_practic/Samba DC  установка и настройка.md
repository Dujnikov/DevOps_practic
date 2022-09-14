           

Перед настройкой пользователя меняем сложность паролей командой:

samba-tool domain passwordsettings set --min-pwd-length=6 --complexity=off --max-pwd-age=0 --min-pwd-age=0

Подготовка 3х пользователей Samba DC

1. aeca1da c паролем aeca1da

2. aeca2da c паролем aeca2da

3. aeca3da c паролем aeca3da

Пароль для пользователя можно задать следующей командой: 
samba-tool user create aeca1da

Отключить учетную запись: **samba****-****tool** **user** **disable aeca1da**

Вывести список групп можно следующей командой: 
samba-tool  group list

Добавление группы: samba-tool group add aecausers

Создадим группы администраторов и пользователей: aecaadmins и aecausers

samba-tool group add aecausers

samba-tool group add aecaadmins

Добавление пользователей в группу:

samba-tool group addmembers aecausers aeca1da

amba-tool group addmembers aecausers aeca2da

samba-tool group addmembers aecausers aeca2da

Проверка входа при помощи учетной записи администратора домена:

smbclient //localhost/netlogon –U Administrator – c ‘ls’