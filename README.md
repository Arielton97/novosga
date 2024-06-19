## Este Readme deve ser seguido no Ubuntu 22.04 server, desktop ou WSL

as pastas neste projeto estão como um arquivo de backup 


### 1 - INSTALAR APACHE2

sudo apt update

sudo apt install apache2

sudo a2enmod rewrite env

sudo service apache2 restart

sudo chmod -R 777 /etc/apache2/

sudo systemctl restart apache2


### 2 - INSTALAR PHP 7.4

sudo apt-add-repository ppa:ondrej/php

sudo apt update

sudo apt install php7.4 php7.4-mysql php7.4-curl php7.4-zip php7.4-intl php7.4-xml php7.4-mbstring

sudo chmod -R 777 /etc/php/


### 3 – Instalar MySQL 5.7 e criar banco de dados

sudo apt install mariadb-server

sudo service mysql start

sudo mysql_secure_installation


Acessar o mysql:

sudo mysql -u root -p

Pode copiar e colar tudo 

CREATE DATABASE novosga_db;
CREATE USER 'novosga_us'@'%' IDENTIFIED BY '123456';
GRANT ALL PRIVILEGES ON novosga_db.* TO 'novosga_us'@'%' IDENTIFIED BY '123456';
FLUSH PRIVILEGES;
exit;

### 4 – Baixar o Composer
export LANGUAGE=pt_BR

php composer.phar create-project "novosga/novosga:^2.1" novosga2

php composer.phar update -d ~/novosga2


MOVER O DIRETÓRIO 
sudo mv novosga2/ /var/www/html/ 

sudo chmod -R 777 /var/www/html/novosga2/


### 5 - PREPARAR O CACHE DA APLICAÇÃO DO PRODUTO 
cd /var/www/html/novosga2/ 

sudo bin/console cache:clear --no-debug --no-warmup --env=prod

sudo bin/console cache:warmup --env=prod


### 6 - ALTERAR O DIRETÓRIO RAIZ E HABILITAR 
sudo sed -i 's|AllowOverride None|AllowOverride All|g' /etc/apache2/apache2.conf

sudo nano /etc/apache2/sites-available/000-default.conf

Insira o seguinte no final do arquivo:

<Directory /var/www/html>
AllowOverride All
</Directory>

Ctrl+O 
Ctrl+X 


### 7 - CRIAR E EDITAR O ARQUIVO htacces 

echo 'Options -MultiViews

RewriteEngine On

RewriteCond %{REQUEST_FILENAME} !-f

RewriteRule ^(.*)$ index.php [QSA,L]

SetEnv APP_ENV prod

SetEnv LANGUAGE pt_BR

SetEnv DATABASE_URL mysql://novosga_us:123456@localhost:3306/novosga_db

' > /var/www/html/novosga2/public/.htaccess




### 8 - CONFIGURAR O TIMEZONE 

sudo echo 'date.timezone = America/Sao_Paulo' > /etc/php/7.4/apache2/conf.d/datetimezone.ini

reiniciar serviço do Apache2:

sudo service apache2 restart


### 9 - COMANDO INSTALL DO NOVOSGA 

APP_ENV=prod \

LANGUAGE=pt_BR \

DATABASE_URL="mysql://novosga_us:123456@localhost:3306/novosga_db" \

bin/console novosga:install

sudo chmod -R 777 /var/www/html/novosga/

preêncha o segundo campo com a senha, e dê enter em todos os outros 



[Instalar o WSL | Microsoft Learn](https://learn.microsoft.com/pt-br/windows/wsl/install)

[How to install Apache2 |Ubuntu](https://ubuntu.com/server/docs/how-to-install-apache2)

[How to install and configure PHP | Ubuntu](https://ubuntu.com/server/docs/how-to-install-and-configure-php)

[Install and configure a MySQL server | Ubuntu](https://ubuntu.com/server/docs/install-and-configure-a-mysql-server)

[Canal do Ezec para quaisquer dúvidas](https://ezectech.com/tutorial/instalacaonovo-sga-2-0-passo-a-passo-no-windows-10/) 


