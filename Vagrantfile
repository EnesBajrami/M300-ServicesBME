# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.define "database01" do |db|
    db.vm.box = "ubuntu/xenial64"
	db.vm.provider "virtualbox" do |vb|
	  vb.memory = "512"  
	end
    db.vm.hostname = "database01"
    db.vm.network "private_network", ip: "192.168.10.100"
    # MySQL Port nur im Private Network sichtbar
	# db.vm.network "forwarded_port", guest:3306, host:3306, auto_correct: false
  	db.vm.provision "shell", path: "db.sh"
  end
  
  config.vm.define "webserver01" do |web|
    web.vm.box = "ubuntu/xenial64"
    web.vm.hostname = "webserver01"
    web.vm.network "private_network", ip:"192.168.10.101" 
	web.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
	web.vm.provider "virtualbox" do |vb|
	  vb.memory = "512"  
	end     
  	web.vm.synced_folder ".", "/var/www/html"  
	web.vm.provision "shell", inline: <<-SHELL
		sudo apt-get update
		sudo apt-get install ufw -y
		sudo ufw allow from 10.0.2.2 to any port 22
		sudo ufw allow 80/tcp
		sudo ufw --force enable
		sudo apt-get install libapache2-mod-proxy-html -y
		sudo apt-get install libxml2-dev -y
		a2enmod proxy
		a2enmod proxy_html
		a2enmod proxy_http
		sed -i '$aServerName localhost' /etc/apache2/apache2.conf
		service apache2 restart
		cd /etc/apache2/sites-enabled
		wget https://pastebin.com/raw/GbjFC2ii
		cp GbjFC2ii 001-reverseproxy.conf
		sudo apt-get -y install debconf-utils apache2 nmap
		sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password 1234'
		sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password 1234'
		sudo apt-get -y install php libapache2-mod-php php-curl php-cli php-mysql php-gd mysql-client  
		# Admininer SQL UI 
		sudo mkdir /usr/share/adminer
		sudo wget "http://www.adminer.org/latest.php" -O /usr/share/adminer/latest.php
		sudo ln -s /usr/share/adminer/latest.php /usr/share/adminer/adminer.php
		echo "Alias /adminer.php /usr/share/adminer/adminer.php" | sudo tee /etc/apache2/conf-available/adminer.conf
		sudo a2enconf adminer.conf 
		sudo service apache2 restart 
	  echo '127.0.0.1 localhost webserver01\n192.168.10.100 database01' > /etc/hosts
SHELL
	end  
 end
