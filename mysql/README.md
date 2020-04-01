Este resolvi aproveitar o oficial

Baixar a imagem
sudo docker pull mysql

sudo docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=root6Beer -d mysql

***********************************************************************
gerando uma variavel no .cnf, como exemplo:

sudo docker exec -it mysql bash 

echo "[mysqld]" >  /etc/mysql/mysql.conf.d/only_full_group_by.cnf

echo "sql_mode = ''" >>  /etc/mysql/mysql.conf.d/only_full_group_by.cnf

service mysql restart


/etc/mysql/conf.d

docker exec -i mysqlstaging0514 /bin/bash -c 'cat >/etc/mysql/conf.d/my,cnf' < my.cnf

*************************
[mysqld]
max_allowed_packet=1024M

sql_mode = ONLY_FULL_GROUP_BY,STRICT_ALL_TABLES,STRICT_TRANS_TABLES,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_AUTO_VALUE_ON_ZERO,NO_ENGINE_SUBSTITUTION

lower_case_table_names = 1

connect_timeout = 120

max_connections = 200

interactive_timeout = 57600

innodb_buffer_pool_size=805306368

innodb_log_file_size=4096M

*************************

# Ajuste erro de password
Authentication plugin 'caching_sha2_password' cannot be loaded: dlopen(/usr/local/mysql/lib/plugin/caching_sha2_password.so, 

docker exec -it CONTAINER_ID bash mysql_upgrade -u root -p

mysql --user=root --password

Enter the password for root (Default is 'root') Finally Run:


ALTER USER 'username' IDENTIFIED WITH mysql_native_password BY 'password';
-----------------------------------------------------------------------------------------

import

docker exec -i container_name mysql -uroot dbname < data.sql;

docker exec -i mysqlpearson mysql -uroot -proot6Beer awplus < Dump20190818Local.sql


#com volume

docker run -v /opt/docker/mysqlOficina/data:/var/lib/mysql -p 3306:3306 --name mysqlOficina -e MYSQL_ROOT_PASSWORD=root6Beer -d mysql

docker run -v /home/crleal/docker/mysqlpearson/data:/var/lib/mysql -p 3306:3306 --name mysqlpearson -e MYSQL_ROOT_PASSWORD=root6Beer -d mysql:5.7


Cria container ignorando case
docker run -v /home/xxxxxx/docker/mysqlpearson/data:/var/lib/mysql -p 3306:3306 --name mysqlpearson -e MYSQL_ROOT_PASSWORD=root6Beer -d mysql:5.7 mysqld --lower_case_table_names=1

*****************************************

Exemplo de phpmyadmin
docker run --rm --link mysqlxxxxx:mysql -p 1234:80 nazarpc/phpmyadmin


docker exec -i ac11cc11af99 mysql -uroot -p"root6Beer" awplus < Dump20190818Local.sql

*********************************************************************************************



