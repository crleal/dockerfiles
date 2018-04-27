Este resolvi aproveitar o oficial

Baixar a imagem
sudo docker pull mysql

*** -p 3306:3306  = localhost:3306


sudo docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=root6Beer -d mysql



gerando uma variavel no .cnf, como exemplo:

sudo docker exec -it mysql bash 

echo "[mysqld]" >  /etc/mysql/mysql.conf.d/only_full_group_by.cnf

echo "sql_mode = ''" >>  /etc/mysql/mysql.conf.d/only_full_group_by.cnf

service mysql restart


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



#com volume

docker run -v /opt/docker/mysqlmain/data:/var/lib/mysql -p 3306:3306 --name mysqlmain -e MYSQL_ROOT_PASSWORD=root6Beer -d mysql:5.6


docker run -v /opt/docker/mysqlmain0226/data:/var/lib/mysql -p 3306:3306 --name mysqlmain0226 -e MYSQL_ROOT_PASSWORD=root6Beer -d mysql:5.6

docker run -v ~/dockerfiles/mysql:/etc/mysql/mysql.conf.d -v /opt/docker/mysqlstaging0426/data:/var/lib/mysql -p 3306:3306 --name mysqlstaging0426 -e MYSQL_ROOT_PASSWORD=root6Beer -d mysql:5.6



Exemplo de phpmyadmin

docker run --rm --link mysqlstaging0426:mysql -p 1234:80 nazarpc/phpmyadmin

