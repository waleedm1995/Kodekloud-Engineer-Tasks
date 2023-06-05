The Nautilus application development team has shared that they are planning to deploy one newly developed application on Nautilus infra in Stratos DC. The application uses PostgreSQL database, so as a pre-requisite we need to set up PostgreSQL database server as per requirements shared below:

a. Install and configure PostgreSQL database on Nautilus database server.

b. Create a database user ```kodekloud_roy``` and set its password to ```ksH85UJjhb```.

c. Create a database ```kodekloud_db7``` and grant full permissions to user ```kodekloud_roy``` on this database.

d. Make appropriate settings to allow all local clients (local socket connections) to connect to the ```kodekloud_db7``` database through ```kodekloud_roy``` user using ```md5``` method (Please do not try to encrypt password with md5sum).

e. At the end its good to test the db connection using these new credentials from root user or server's sudo user.

```
yum -y install postgresql-server postgresql-contrib
postgresql-setup initdb
systemctl enable postgresql
systemctl start postgresql
sudo -u postgres psql
CREATE USER kodekloud_roy WITH PASSWORD 'ksH85UJjhb';
CREATE DATABASE kodekloud_db7;
GRANT ALL PRIVILEGES ON DATABASE "kodekloud_db7" to kodekloud_roy;
vi /var/lib/pgsql/data/postgresql.conf
      listen_addresses = 'localhost'                                          # uncomment it
vi /var/lib/pgsql/data/pg_hba.conf
      local   all             all             md5                       peer
      host    all             all             127.0.0.1/32              md5      
      host    all             all             ::1/128                   md5      
cat /var/lib/pgsql/data/pg_hba.conf |grep md5
psql -U kodekloud_roy -d kodekloud_db7 -h 127.0.0.1 -W
      \q
psql -U kodekloud_roy -d kodekloud_db7 -h localhost -W
```


