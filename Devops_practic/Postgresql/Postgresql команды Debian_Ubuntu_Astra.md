Debian/Ubuntu/Astra          

			sudo apt install postgresql-11 - установка postgres на debian системы (Centos - sudo yum (dnf) install postgresql)
		   
		   sudo systemctl restart [[Postgresql]] команды CentOS_RedOS postgresql - перезапуск postgres
		   
		   sudo systemctl stop postgresql - остановить postgres
		              
		   sudo systemctl status postgresql - мониторинг работы postgres
		   
		   sudo -i -u postgres - вход в podtgres под пользователем postgres
		   
		   psql - вход в postgres
		   
		   psql -d aecatest - вход в базу данных (в данном случае название aeca)
		   
		   \d - просмотр таблиц БД
		   
		   \l - просмотр БД
		   
		   \q - выход из postgres
		   
		   \с "postgres" переход на другую бд
		   
		   psql -Uaeca -W aecatest - проверка входа в БД (в данном случае пользователь "aeca", БД - "aecatest")
		   
		   CREATE TABLE tutorials (id int, tutorial_name text); - создание таблицы, "tutorials" - название таблицы, (id int, tutorial_name text) - параметры
		   
		   DROP TABLE TableNameHere; - удаление таблицы, где "TableNameHere" - имя таблицы. Можо удалять таблицы путем вставки их по порядку и через запятую 
		   (DROP TABLE TableNameHere, aecatest, tablesfornetwork, workspace;) 
		   
		   DROP TABLE TableNameHere CASCADE; - удаление с последовательностью таблиц
		   
		    createuser aeca -P - создание пользователя, где "aeca" имя пользователя
			
			createdb aecatest -O aeca - создание БД, где "aecatest", "aeca" - пользователь этой БД
			
			ALTER DATABASE name OWNER TO new_owner; - смена владельца базы данных
			
			GRANT ALL PRIVILEGES ON DATABASE "database1" to dmosk; - смена прав на работу в бд postgres пользователя (dmosk)
			
			Для успешного подключения локально пользователя в базу надо отредактировать файл **/etc/postgresql/11/main/pg_hba.conf,** найти строку **local all all** **peer** и изменит на **local all all trust,** сохранить изменения и перезапустить postgres
		   
		    psql -d aecatest -f create-tables-ejbca-postgres.sql - запустить sql при помощи postgres
		   