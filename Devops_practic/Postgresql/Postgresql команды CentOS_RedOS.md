

     	dnf update
    	dnf install postgresql-server
    	postgresql-setup --initdb
		Заходим по адресу /var/lib/pgsql/data/pg_hba.conf
		 В подключениях меняем ident на password
		 
		local   all             all                            ident
	# IPv4 local connections:
	host    all             all             127.0.0.1/32    password 
	# IPv6 local connections:
	host    all             all             ::1/128         password
    	
		systemctl start postgresql
    	systemctl enable postgresql
   		sudo -i -u postgres
        psql
		CREATE USER aeca;
		ALTER USER aeca WITH PASSWORD 'aeca';
		CREATE DATABASE aecatest;
		ALTER DATABASE aecatest OWNER TO aeca;
		GRANT ALL PRIVILEGES ON DATABASE "aecatest" to aeca;
		ALTER USER aeca SUPERUSER;
		\q
	    systemctl restart postgresql 
  
   psql -U aeca -h localhost

   13  psql -Uaeca -W aecatest
   15  mc
   16  systemctl restart postgresql
   17  systemctl status postgresql
