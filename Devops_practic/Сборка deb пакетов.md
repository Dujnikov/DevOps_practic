
В рассмотренном ниже примере мы создадим один deb пакет с аж тремя вкусными штуками:  
1) конфигурационные файлы nginx с нашего сервера  
2) файл с public ключами для авторизации обладателей закрытой части этих ключей на сервере рутом  
3) скрипт /usr/bin/ourscript.sh (неважно что он делает, по сути)

Принцип одинаковый, просто мне удобно показать сразу три примера. Пакет будет называться nginxsuperconfig

Предрекая вопросы «а зачем тебе fakeroot, если всё делаешь рутом?». **Удобно**. А главное — просто и быстро.

Начнем-с с создания нужных каталогов и копирования в эту структуру нужных нам файлов. Каталог DEBIAN должен быть написан именно большими буквами. Остальные каталоги — воссоздание структуры необходимых нам файлов с условным корнем в виде каталога /root/builder/nginxsuperconfig/. То есть всё, что лежит в этом каталоге (кроме DEBIAN) просто распакуется в корень. Как будто вы создадите tarболл с содержимым этого каталога и распакуете его в корень.  
`**root@builder:~# mkdir -p /root/builder/nginxsuperconfig/DEBIAN  
root@builder:~# mkdir -p /root/builder/nginxsuperconfig/etc  
root@builder:~# mkdir -p /root/builder/nginxsuperconfig/usr/bin  
root@builder:~# mkdir -p /root/builder/nginxsuperconfig/root/.ssh  
root@builder:~# cp -r /etc/nginx /root/builder/nginxsuperconfig/etc  
root@builder:~# cp /usr/bin/ourscript.sh /root/builder/nginxsuperconfig/usr/bin/  
root@builder:~# cp /root/.ssh/authorized_keys /root/builder/nginxsuperconfig/root/.ssh/**`

Теперь нам понадобится написать файлы, описывающие свойства пакета. Обязательным является только файл DEBIAN/control. Для примера я ещё напишу несколько скриптов — один из них будет выполняться перед установкой пакета, второй — по окончанию и ещё один — при удалении пакета.

Напишем файл control:  
`**root@builder:~# editor /root/builder/nginxsuperconfig/DEBIAN/control**`  
Я перечислю обязательные поля. На самом деле туда можно много чего написать, но это уже лучше поискать в сети:  
_`Package: nginxsuperconfig  
Version: 1.0-1  
Section: misc  
Priority: extra  
Maintainer: inkvizitor68sl  
Architecture: all  
Depends: nginx, openssh-server, bash  
Description: Example package  
Package with nginx configs, ssh keys, example script.`_

Немного прокомментирую.  
Package — название пакета.  
Version — версия. Через дефис пишем «номер сборки». Например, если вы слегка поправили файл в содержимом, но версия пакета не сменилась. В данном случае мы сами решаем какая у нас версия, потому можно не париться и всегда ставить версия-1  
Section — для случаев рассмотренных в примере больше всего подходит misc  
Priority — аналогично, подходит extra  
Maintainer — ваше имя/ник и почта  
Depends — в простейшем случае через запятые перечисляем имена пакетов, которые должны быть установлены, чтобы ваш пакет работал. В нашем случае — nginx (мы же для него конфиг льем), openssh-server (а зачем ключи, если ssh сервера нет?), bash, без которого не запустится наш скрипт.  
Description — строка с кратким описанием пакета (не более 70 символов). Следующие строки — полное описание пакета. Перенос строки — точка.

Теперь создадим нужные скрипты.  
Выполняемый перед инсталляцией:  
`**root@builder:~# editor /root/builder/nginxsuperconfig/DEBIAN/preinst**`  
`_#!/bin/bash  
mv /etc/nginx /etc/nginx.bak  
mv /root/.ssh/authorized_keys /root/.ssh/authorized_keys.old_`

Выполняемый после инсталляции:  
`**root@builder:~# editor /root/builder/nginxsuperconfig/DEBIAN/postinst**`  
_`#!/bin/bash  
/etc/init.d/nginx restart  
chmod +x /usr/bin/ourscript.sh`_

Выполняемый после удаления:  
`**root@builder:~# editor /root/builder/nginxsuperconfig/DEBIAN/postrm**`  
`_#!/bin/bash  
rm -r /etc/nginx  
mv /etc/nginx.bak /etc/nginx  
rm /root/.ssh/authorized_keys  
mv /root/.ssh/authorized_keys.old /root/.ssh/authorized_keys_`

Ещё можно создать выполняемый перед удалением скрипт:  
`**root@builder:~# editor /root/builder/nginxsuperconfig/DEBIAN/prerm**`

В общем-то всё готово к сборке пакета:  
`**root@builder:~# cd /root/builder/  
root@builder:~# fakeroot dpkg-deb --build nginxsuperconfig**`  
Мы получим файл nginxsuperconfig.deb. Неплохо его ещё переименовать, чтобы в названии содержалась версия:  
`**root@builder:~# mv nginxsuperconfig.deb nginxsuperconfig_1.0-1.deb**`