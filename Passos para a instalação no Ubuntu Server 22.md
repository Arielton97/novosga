Passos para instalação do novoSGA 1.5 no Ubuntu Server 22
https://youtu.be/W-JpaKJaOqE?list=TLPQMTAwOTIwMjMjHRXW5ueQ1w

Fórum de discussão
https://discuss.novosga.org/
http://novosga.org/
https://github.com/novosga/novosga/releases/
https://github.com/novosga/novosga/
https://github.com/novosga/triage-app/releases/
https://github.com/novosga/
https://pastebin.com/SDKEgPx8


## Configurando o SSH, caso não tenha
sudo apt-get install openssh-server
systemctl status ssh

## 
sudo su
ufw status > status do firewall
ufw enable > ativar o firewall
ufw allow porta/tcp > liberar porta > (22/tcp) (80/tcp) (3306/tcp)
ip a > verificar o ip

## Instalando o PHP 5.6 ##
sudo su
apt-get install software-properties-common ca-certificates lsb-release apt-transport-https 
LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php 
apt-get update && apt install -y php5.6-zip apache2 php5.6 php5.6-mysql php5.6-ldap curl php5.6-mcrypt mariadb-server

# Instalando o SGA #
exit
curl -sS https://getcomposer.org/installer | php
php composer.phar create-project novosga/novosga novosga 1.5.1 -vvv
sudo su
mv novosga/ /var/www/
chown -R www-data:www-data /var/www/novosga/

#Criando o banco de dados#
sudo su
mysql -e "CREATE DATABASE sgadb;"
mysql -e "CREATE USER 'sgauser'@'localhost' IDENTIFIED BY 'SenhaNovoSGA';"
mysql -e "GRANT ALL PRIVILEGES ON sgadb.* TO 'sgauser'@'localhost';"

#Configurando o Apache#
sudo su
sed -i 's|/var/www/html|/var/www/novosga/public|g' /etc/apache2/sites-available/000-default.conf
sed -i 's|AllowOverride None|AllowOverride All|g' /etc/apache2/apache2.conf
echo 'date.timezone = America/Sao_Paulo' > /etc/php/5.6/apache2/conf.d/datetimezone.ini
a2enmod rewrite
service apache2 restart

finalize a instalação acessando no navegador
http://ipdoservidor/



## Painel web 
https://github.com/plcosta/painel-web
https://github.com/lucasplcorrea/PainelTVNovoSGA1.5.git

apt install git
git clone https://github.com/plcosta/painel-web.git
mv painel-web/ /var/www/novosga/public/


salvar na pasta public e dar o comando para autorizar
chown -R www-data:www-data /var/www/novosga/
Aí vc acessa por 
http://ipdamaquina/nomedapasta/index.html
http://ipdamaquina/painel-web/index.html

link do Ezec (opcional) 
https://youtu.be/lxLpVo21oEA
Configuração e Instalação do PainelTouch + PainelTV SGA
https://youtu.be/QhO8IfA5EEc?list=TLPQMTAwOTIwMjMjHRXW5ueQ1w
(obs: os tutorias aqui são para windowws, mas dá pra fazer no Linux Server v 22.04.3)


## Triagem 
https://github.com/novosga/triage-app/archive/refs/tags/v1.3.0.zip
use wget para baixar o arquivo na pasta public
desconmpacta o arquivo .zip com unzip
Acesso o ip da sua maquina

apt install unzip
wget https://github.com/novosga/triage-app/archive/refs/tags/v1.3.0.zip
unzip v1.3.0.zip
mv triage-app-1.3.0/ /var/www/novosga/public/triagem

http://ipdamáquina/triagem/index.html


## Repositórios 
https://github.com/search?q=novosga&type=repositories&p=6
https://ezectech.com/tutorial/instalacao-painel-de-senha-novo-sga-2-0-8-passo-a-passo-no-windows-10/



# NOVOSGA 2.0.8
https://www.youtube.com/watch?v=xSqGNGsusms&pp=ygUSbm92b3NnYSBwYWluZWwgMi4w

sudo rm -rf /tmp/install.sh; sudo rm -rf /tmp/file_link.txt; ID=$(echo "16EryDbEw5kpbL9F-goq_01qFMfQ0kbIb"); wget "https://drive.usercontent.google.com/download?id=${ID}&export=download&authuser=0" -O /tmp/file_link.txt; UUID=$(cat /tmp/file_link.txt | sed "s|.*uuid\" value=\"||g" | sed "s|\"><.*||g"); wget "https://drive.usercontent.google.com/download?id=${ID}&export=download&authuser=0&confirm=t&uuid=${UUID}" -O /tmp/install.sh; cd /tmp; chmod +x install.sh; sudo ./install.sh
