# ScriptLinux
Script Linux Apache 


###
## Fazendo Download dos programas necessarios Apache, PHP e Mysql
###

down="http://apache.usp.br/httpd/httpd-2.0.50.tar.gz http://br.php.net/distributions/php-4.3.8.tar.gz http://www.linorg.usp.br/mysql/Downloads/MySQL-4.0/mysql-4.0.20.tar.gz"
for download in $down
do
  $wget $parametros $download
done

## Instalando Programas
###
sleep 5s ; 

#
# Descompactando os pacotes, usando um for, por sugestão do NoComments
#

packs="httpd-2.0.50.tar.gz php-4.3.8.tar.gz mysql-4.0.20.tar.gz"

for desc in $packs
do
  echo "descompactando $desc" 
  sleep 5s
  tar $paratar $desc
done

#
# Instalando os pacotes
#

echo "Instalando o MySQL"
cd $mysql ;
$config $paramysql && sleep 5s && $make && $make install ;

echo "Completada a instalacao do MySQL!"
sleep 10s; 

echo "Instalando Apache"
cd $apache ;
$config $parahttpd && sleep 5s && $make && $make install ; 

echo "Completada a instalacao do apache" ;
sleep 10s;

echo "Instalando o php"
cd $php ;
$config $paraphp && sleep 5s && $make && $make install ;

echo "Completada a instalacao do PHP"
sleep 10s; 

echo "configurando o MySQL"
echo "sera executado o programa mysql_secure_installation, para fazer uma instalacao segura"
echo "primeiro vai criar o banco de dados com o mysql_install_db"
echo "No mysql_secure_installation irao aparecer algumas perguntas, responda de acorod com sua necessidade"
echo "apos terminar a configuracao, execute /usr/local/apache2/bin/apachectl start para iniciar o apache"
echo "quando precisar iniciar o mysql, use mysqld_safe & "

sleep 10s;
ln -s $mysqlinstall/bin/mysqld_safe /sbin/mysqld_safe ;
ln -s $mysqlinstall/bin/mysql /sbin/mysql ;
$mysqlinstall/bin/mysql_install_db ;
chown $parachown $mysqlinstall/var ;
$mysqlinstall/bin/mysqld_safe & ;
$mysqlinstall/bin/mysql_secure_installation ; sleep 15s ;
