# bash-scripts
# WSL  
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart  
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux  
sudo nano /etc/wsl.conf  
[automount]  
enabled = true  
options = "metadata,umask=22,fmask=11"  
  
  for wsl work fast  
sudo nano /etc/nginx/nginx.conf  
fastcgi_buffering off;  
  
### WSL conf ###  
.wslconfig file in C:\Users\username  
[wsl2]  
memory=6GB # Limits VM memory in WSL 2 to 4 GB  
processors=6 # Makes the WSL 2 VM use two virtual processors  
  
# Install php environment
sudo add-apt-repository ppa:ondrej/apache2 php  
sudo apt install php7.4  
sudo apt install composer  
sudo apt install nginx  
sudo apt install mysql-server   
  
sudo apt install php7.4-curl php7.4-json php7.4-readline php7.4-xml php7.4-intl php7.4-gd php7.4-zip php7.4-mbstring php7.4-mysql php7.4-pgsql php7.4-opcache php7.4-fpm  
  
sudo apt install postgresql  
sudo -u postgres psql -U postgres  
  \# CREATE USER username WITH ENCRYPTED PASSWORD 'put-your-password-here';  
  \# CREATE DATABASE dbname owner username;  
  
Yii assets composer fix
```
"repositories": [
    {
        "type": "composer",
        "url": "https://asset-packagist.org"
    }
]
```
  
# Phalcon  
php vendor/bin/phalcon migration run --config=config/config_master.yml  
php vendor/bin/phalcon migration run  
php vendor/bin/phalcon model --name=Vacancies --get-set  
  
docker-compose down && docker network rm app_site_http_network && docker-compose up -d --force-recreate  
docker system prune --all  
  
---TA-DA containers---  
docker exec -it api_api-prod_1 bash  
docker exec -it api_mysql-master_1 bash  
supervisorctl restart workers:*  
  
список воркеров гирмана, их статус  
gearadmin --status  

просмотр процессов  
supervisorctl status  

перезапуск воркеров  
supervisorctl restart workers:CategoriesWorker_00 workers:CategoriesWorker_01  

аналогично перезапуск процессов  
supervisorctl restart gearman  

если был измене конфиг супервизора  
supervisorctl update all  

очистить очередь гирман  
/usr/bin/gearman -t 1000 -n -w -f indexGoodReindex > /dev/null  
  
# Vue.js env  
curl -fsSL https://deb.nodesource.com/setup_current.x | sudo -E bash -  
sudo apt-get install -y nodejs  
sudo apt install nodejs  
sudo apt install npm  
  
yarn global add @vue/cli @vue/cli-service-global  
vue create hello-world  
  
---yarn---  
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -  
or curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -  
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list  
sudo apt-get update  
sudo apt-get install yarn  
  
curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo  
sudo rpm --import https://dl.yarnpkg.com/rpm/pubkey.gpg  
yum install yarn  
  
  
Use n module from npm in order to upgrade node  
  
sudo npm cache clean -f  
sudo npm install -g n  
sudo n stable  
To upgrade to latest version (and not current stable) version, you can use  
  
sudo n latest  
  
# Git  
git config --global credential.helper store  
git config --global core.autocrlf false  
git config --global core.fileMode false  
  
git update-index --assume-unchanged filename  
 git reset --soft HEAD~  
  
git-credential-manager.exe uninstall  
Run this command in C:\Program Files\Git\mingw64\libexec\git-core  
  
nano ~/.ssh/config  
Host bitbucket.org  
    Hostname bitbucket.org  
    IdentityFile ~/.ssh/rsa  
    IdentitiesOnly yes  
    
  Host github.com  
    Hostname github.com  
    User git  
    IdentityFile C:\Users\immortal\.ssh\id_rsa  
# Golang  
packages:  
go get github.com/gorilla/websocket && go get github.com/isayme/go-amqp-reconnect/rabbitmq && go get github.com/fatih/structs && go get github.com/jmoiron/sqlx && go get github.com/go-sql-driver/mysql && go get github.com/araddon/dateparse && go get github.com/mitchellh/mapstructure  
go tool pprof http://localhost:6060/debug/pprof/heap  
apt install graphviz // for UI  
  
import _ "net/http/pprof"  
go func() {  
	http.ListenAndServe("localhost:6060", nil)  
}()  
  
# Mysql
sudo nano /etc/apt/sources.list  
 \# deb http://repo.mysql.com/apt/ubuntu bionic mysql-5.7
  
sudo nano /etc/mysql/my.cnf  
[mysqld]  
default_authentication_plugin= mysql_native_password  
  
CREATE USER 'test_user'@'localhost' IDENTIFIED BY 'password';  
GRANT ALL PRIVILEGES ON \*.\* TO test_user@localhost;  
ALTER USER 'test_user'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';  
  
# systemd service
journalctl -u servicename -f  
sudo nano /etc/systemd/system/service_name.service  
[Unit]  
Description=  
After=network.target  
  
[Service]  
Type=simple  
ExecStart=  
WorkingDirectory=  
User=web  
Group=web  
Restart=always  
RestartSec=10  
  
[Install]  
WantedBy=multi-user.target  
  
sudo systemctl enable your_name && sudo service your_name start;  
# Linux Repo and commands
https://releases.ubuntu.com/20.04/ubuntu-20.04.2-live-server-amd64.iso  
  
no password on sudo  
sudo nano /etc/sudoers.d/filename  
\# username     ALL=(ALL) NOPASSWD:ALL  
  
/usr/bin/flock -xn /var/lock/import.lock -c 'sh /root/import.sh'  
  
sudo apt-get install \  
    apt-transport-https \  
    ca-certificates \  
    curl \  
    gnupg-agent \  
    software-properties-common  
    
---- Clean disk usage commands ------  
sudo apt-get autoremove  
sudo du -sh /var/cache/apt  
sudo apt-get autoclean  
sudo apt-get clean  
journalctl --disk-usage
sudo journalctl --vacuum-time=3d  
  
wget https://getcomposer.org/composer.phar  
mv composer.phar /usr/local/bin/composer  
chmod +x /usr/local/bin/composer  
chown apache /usr/local/bin/composer  
setxkbmap -layout us,ua  
setxkbmap -option 'grp:alt_shift_toggle'  
  
setfacl -d -m o::rwx your/directory/path  
  
# combine pdfs  
sudo apt install poppler-utils  
pdfunite file1.pdf file2.pdf mergedfile.pdf  
  
