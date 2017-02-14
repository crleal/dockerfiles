Este resolvi aproveitar o oficial

Baixar a imagem
sudo docker pull mysql

*** -p 3306:3306  = localhost:3306


sudo docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=root6Beer -d mysql



serando uma variavel no .cnf, como exemplo:

sudo docker exec -it mysql bash 
echo "[mysqld]" >  /etc/mysql/mysql.conf.d/only_full_group_by.cnf
echo "sql_mode = ''" >>  /etc/mysql/mysql.conf.d/only_full_group_by.cnf

service mysql restart



