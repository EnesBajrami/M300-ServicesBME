# **Modul 300 LB1 Dokumentation** 

# Inhaltsverzeichnis
  - [01 - Umgebung](#01---umgebung)
  - [02 - Verwendetet Tools](#02---verwendetet-tools)
  - [03 - Wissenstand](#02---wissenstand)
    - [03.1 - Linux](#03.1---linux)
    - [03.2 - Virtualisierung](#03.2---virtualisierung)
    - [03.3 - Vagrant](#03.3---vagrant)
    - [03.4 - Versionverwaltung/Git](#03.4---versionverwaltunggit)
    - [03.5 - Markdown](#03.5---markdown)
    - [03.6 - Systemsicherheit](#03.6---systemsicherheit)
  - [04 - Lernschritte](#04---lernschritte)
    - [04.1 - Vagrant](#04.1---Vagrant)
    - [04.2 - Netzwerkplan](#04.1---netzwerkplan)
    - [04.3 - Installation - Webserver - und -Datenbank](#04.1---installation - Webserver - und - Datenbank)
  - [05 - Sicherheitsaspekte](#04.1---Sicherheitsaspekte)
    - [05.1 - UFW - Firwall](#04.1---UFW-Firewall)
    - [05.2 - Reverse-Proxy](#04.1---Reverse-Proxy)
    - [05.3 - SSH-Tunnel](#04.1---SSH-Tunnel)
    - [05.4 - Webserver per HTTPS sichern](#04.1---Webserver per HTTPS sichern)
  - [06 - Wissenzuwachs](#04.1---Wissenzuwachs)
  - [07 - Reflektion](#04.1---Reflektion)


##Vagrantfile 
Als aller erstes habe ich eine Multi-VM Umgebung aufgebaut. Der dazugehörige code für die erstellten verschiedenen VM's sind alle im Vagrantfile vorhanden. Drinnen im Vagrant-File ist alles genaustens beschrieben wie die Abfolge funktioniert und welche Schritte gemacht werden. Für die VM's habe ich immer Ubuntu 16.04 verwendet, da ich mich mit dieser Distrubution sehr gut auskenne. 


##DHCP-Server
Einer dieser VM's ist ein DHCP-Server der sehr einfach gehalten ist, damit es zur keiner Verwirrrung kommt. Die verschiedenen Spezifikationen können selbsverständlich im Vagrant-File leicht angepasst werden. 


    IP: 192.168.20.5
    Hostname: dhcp
    RAM: 1024 MB
    Operating System: Linux (Ubuntu)

Hier sieht man noch einen Abschnitt vom Vagrant File, wie das ganze realisiert worden ist, sprich nur der Aufbau der VM.

config.vm.define "dhcp" do |dhcp|
  dhcp.vm.box = "ubuntu/xenial64"
  dhcp.vm.hostname = "dhcp"
  dhcp.vm.network "private_network", ip:"192.168.20.5" 
	dhcp.vm.provider "virtualbox" do |vb|
	  vb.memory = "1024"  
end  

##FTP-Server

##Apache-Server mit MYSQL Database






## 01 - Umgebung
* Vagrant
* Visual Studio Code
* Virtual Box 6.0
* Git-Client (Git-Kraken)
* VM

## 02 - Verwendetet Tools
* Virtualbox 6.0
* Vagrant
* Visual Studio Code
* Git-Client (SSH-Key)

## 03 - Wissenstand
### 03.1 - Linux
 Da ich im Betrieb sehr viel zu tun habe mit diversen Linux-Server, bin ich im Thema Linux sehr gut unterwegs. Ich habe schon Erfahrungen gesammelt mit DHCP, DNS und Web-Server. Da wir im Geschäft hauptsächlich mit Virtuellen Maschinen arbeiten, sprich ESXi-Server und Vmware Web-Client schon diverse Projekte hatte. Aber ich bin mir jetzt sehr wohl bewusst für was die einzelnen Softwares für eine Funktion haben und wieso es so wichtig ist für die Systemsicherheit, falls dein PC verloren geht SSD/HDD abstürzt trotzdem immernoch im GIT Repository drauf ist. 

### 03.2 - Virtualisierung
Erfahrung in Virtualisierung mit ESXi, VMware und Virtual Box. Server Umgebungen Virtualisierung im Betrieb geplant und ausgeführt. 

### 03.3 - Vagrant
Mit Vagrant hatte ich bisher noch gar keine Erfahrungen gehabt, sowie bei der Versionsverwaltung, da ich im Geschäft sehr wenig mit Skripten zu tun habe.

### 03.4 - Versionverwaltung/Git
Erfahrung im Betrieb mit Versionverwaltung Document Management Systemen und Cloud. Mit GitHub noch wenige Erfahrungen gemacht. Grundsätzlich sollte es mir nicht schwer fallen mit GitHub zu arbeiten. 

### 03.5 - Markdown
Mark Down hatte ich bisher auch keine Erfahrungen.

### 03.4 - Systemsicherheit
Diverse Firewalls bereits im Betrieb konfiguriert angepasst etc. In unserem Geschäft benutzen wir die Linux basierte Firewall Barracuda, die jedoch kostenpflichtig ist, die Konfiguration wird alles im Web-GUI erstellt. Jedoch musste ich bei anderen Umgebung eine eigen Firewall einrichten und eine Planung erstellen für die Systemsicherheit im Geschäft, sowie in der Schule. Im Betrieb musste ich diverse Firwalls aufsetzen und konfigurieren, bis zur Firewalls mit Grafischer Obefläche (OPNsense usw.) aber auch Firewalls nur auf CML Basis. Ich musste eine Firewall erstellen mit einer Linux Gentoo VM und dort mussten die Firewall-Rules alles Manuell eingegeben werden, was ziemlich mühsam war, aber jedoch sehr profitieren konnte da ich so besser verstanden habe wie eine Firewall wirklcih funktioniert. Ausserdem habe ich mir die Sache sehr erleichtert indem ich ein Skript geschrieben habe, wo dort alles Reglen bereits aufgeschrieben sind, somit haben ich ein besseren Überblick gehabt. 

Aber ich bin mir jetzt sehr wohl bewusst für was die einzelnen Softwares für eine Funktion haben und wieso es so wichtig ist für die Systemsicherheit, falls dein PC verloren geht SSD/HDD abstürzt trotzdem immernoch im GIT Repository drauf ist. 

## 04 - Lernschritte

### 04.1 - Vagrant

**Befehle**

  *vagrant init* - Damit wird im aktuellen Verzeichnis die Vagant-Umgebung initialisiert
  *vagrant up* - Das Vagrantfile wird gelesen und die VMs werden erstellt
  *vagrant ssh* - Baut eine SSH-Verbindung zur gewünschten VM auf
  *vagrant status* - Zeigt den aktuellen Status der VM an
  *vagrant port* - Zeigt die Weitergeleiteten Ports der VM an
  *vagrant halt* - Stoppt die laufende Virtuelle Maschine
  *vagrant destroy* - Stoppt die Virtuelle Maschine und zerstört sie.

**Bestehende VM aus Vagrant Cloud erstellen (Webserver und Datenbank)**
1. Mit *vagrant init* Vagrantfile im gewünschten Verzeichnis erstellt.
2. OS auswhlen von der Cloud https://app.vagrantup.com/boxes/search Ubuntu/xenial64 für meine VM usgewählt.
3. Vagrantfile mit den entsprechenden Parameter erstellen
4. Mit dem Befehl *vagrant up* werden nun die Virtuellen Maschinen erstellt

### 04.2 - Netzwerkplan


    +---------------------------------------------------------------+
    ! Notebook - Schulnetz 10.x.x.x und Privates Netz 192.168.10.1  !                 
    ! Port: 443 (192.158.10.51:443)                                 !	
    !                                                               !	
    !    +--------------------+          +---------------------+    !
    !    ! Web Server         !          ! Datenbank Server    !    !       
    !    ! Host: webserver01  !          ! Host: database01    !    !
    !    ! IP: 192.168.10.51  ! <------> ! IP: 192.168.10.50   !    !
    !    ! Port: 443          !          ! Port 3306           !    !
    !    ! Nat: -             !          ! Nat: -              !    !
    !    +--------------------+          +---------------------+    !
    !                                                               !	
    +---------------------------------------------------------------+


### 04.3 - Installation Webserver und Datenbank
Web Server mit Apache und MySQL User Interface Adminer und Datenbank Server mit MySQL.
Für die Installation der beiden VMs wurde ein Vagrantfile erstellt, in dem alle Angaben wie IP, Hostname, OS etc. befindet. Ausserdem befindet sich ein Shellscript das auf der Datenbankserver MySQL installiert. Auf dem Webserver wurde Apache installiert und auf dem Datenbankserver «Adminer SQL» um die Dantebank über das Web zu verwalten. 
Das Userinterface ist über https://192.168.10.101/adminer.php erreichbar mit dem User 'admin' anmelden. 

### 05 - Sicherheitsaspekte
Beim Sicherheitsaspekt wurde folgende Einstellungen gemacht.

### 05.1 - UFW Firewall

Ausgabe der offenen Ports
    $ netstat -tulpen

Installation
    $ sudo apt-get install ufw

Start / Stop
    $ sudo ufw status
    $ sudo ufw enable
    $ sudo ufw disable

Firewall-Regeln
    # Port 80 (HTTP) öffnen für alle
    vagrant ssh web
    sudo ufw allow 80/tcp
    exit

    # Port 443 (HTTPS) öffnen für alle
    vagrant ssh web
    sudo ufw allow 443/tcp
    exit

    # Port 22 (SSH) nur für den Host (wo die VM laufen) öffnen
    vagrant ssh web
    sudo ufw allow to any port 22
    exit

    # Port 3306 (MySQL) nur für den web Server öffnen
    vagrant ssh database
    sudo ufw allow from 192.168.10.100 to any port 3306
    exit

Zugriff testen
    $ curl -f 192.168.10.101
    $ curl -f 192.168.10.100:3306

### 05.2 - Reverse-Proxy

    Installation Dazu müssen folgende Module installiert werden:
    $ sudo apt-get install libapache2-mod-proxy-html
    $ sudo apt-get install libxml2-dev

Anschliessend die Module in Apache aktivieren:
    $ sudo a2enmod proxy
    $ sudo a2enmod proxy_html
    $ sudo a2enmod proxy_http

Die Datei /etc/apache2/apache2.conf wie folgt ergänzen:
    ServerName 192.168.10.101 

Apache-Webserver neu starten:
    $ sudo service apache2 restart

**Weiterleitung einrichten** 

Die Weiterleitungen sind z.B. in sites-enabled/001-reverseproxy.conf eingetragen:

    # Allgemeine Proxy Einstellungen
    ProxyRequests Off*
    <Proxy>
        Order deny,allow
        Allow from all
    </Proxy>

    # Weiterleitungen master
    ProxyPass /master http://master
    ProxyPassReverse /master http://master


### 05.3 - SSH-Tunnel




### 05.4 - Webserver per HTTPS sichern

    # Default Konfiguration in /etc/apache2/sites-available freischalten (wird nach sites-enabled verlinkt
    sudo a2ensite default-ssl.conf

    # SSL Modul in Apache2 aktivieren
    sudo a2enmod ssl

    # Optional HTTP deaktivieren
    sudo a2dissite 000-default.conf 

    # Datei /etc/apache2/ports.conf editieren und <Listen 80> durch Voranstellen von # deaktivieren
    sudo nano /etc/apache2/ports.conf

    # Unter default-ssl.conf die Server IP eintragen 
    sudo nano /etc/apache2/sites-available/default-ssl.conf
    <IfModule mod_ssl.c>
        <VirtualHost _default_:443>
                ServerName 192.168.10.101

                DocumentRoot /var/www/html

                ErrorLog ${APACHE_LOG_DIR}/error.log
                CustomLog ${APACHE_LOG_DIR}/access.log combined

                SSLEngine on

                SSLCertificateFile      /etc/ssl/certs/apache-selfsigned.crt
                SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key

                <FilesMatch "\.(cgi|shtml|phtml|php)$">
                                SSLOptions +StdEnvVars
                </FilesMatch>
                <Directory /usr/lib/cgi-bin>
                                SSLOptions +StdEnvVars
                </Directory>

        </VirtualHost>
  </IfModule>

    # Apache Server neustarten
    sudo service apache2 restart



### 06 - Wissenszuwachs

**Linux**
Hat sich nicht gross gesteigert, da ich bereits sehr gute Kenntnisse hatte und viel Erfahrungen mit Linux habe. Das einziege was ich mitnehmen konnten, waren die lokalen Firwall-Regeln der Rest war mir von Anfang an bereits bekannt. 

**Virtualisierung**
Bei der Virtualisierung war mein Vorwissen schon recht gut, da ich schon bereits mit jeder Virtaulisierung-Umgebung gearbeitet habe und sehr gut kenne. Ich konnte noch Zusätlich mehr Wissen über VirtualBox mitnehmen, da ich Persönlich mit dem VMware Player arbeite, aber in Prinzip sind sich beide sehr Ähnlich. Für mich Persönlich finde ich das VMware-Player viel flüssiger läuft und besser Gestalltet ist. Hatte bisher wenig Komplikationen mit VirtualBox bin deshlab auch erstaunlicherweise in positiven Sinne erstaunt. 

**Vagrant**
Vagrant war für mich Komplett neuland. Anfangs habe ich noch nichts vestanden, aber mit der Zeit wurde mir immer mehr bewusst für was es genau gebraucht wird und wie vielfältig diese Software ist. Bin sehr erstaunt, was man alles mit Vagrant in kurzer Zeit erstellen kann. Ich habe mir sogar vorgenommen Zuhause eine Umgebung komplett mit Vagrantfiles zu erstellen, da es mich sehr begeistert hat. 

**Versionverwaltung/Git**


**Markdown**
Auch hier war Markdown für mich komplett neuland, bin aber damit sehr gut zurecht gekommen. Ich habe schnell dazu gelernt und wusste genau wie ich die Hashtags einsetzen kann. Anfangs habe ich mir alles komplett im OneNote aufgeschrieben und diese dann im Markdown kopiert, was auch kein problem dargestellt hat. 

**Systemsicherheit**

### 07 - Reflektion
Die LB01 verlief im Grossen ganzen sehr gut. Meiner Meinung nach hatten wir für die LB01 zu wenig Zeit, da die meisten von uns noch nicht alles genau verstanden hat wie Vagrant überhaupt funktioniert, welche Zusammenhang es hatte usw. Darum war ich sehr im Stress, da ich auch schauen musste das meine Umgebung überhaupt funktioniert. Hatte viele Probleme, da sich auch VirtualBox anfangs nciht funkutionierte und musste deshalb immer wieder neu installieren und somit auch viel zeit verloren ging. Ausserdem fand ich noch schwierig ein VagrantFile komplett selbst zu erstellen eine grosse Herausforedung, da es für mich komplett neuland war. Es kam mir so vor wie als würde ein Applikationsentwickler mir einen Auftrag erstellt eine Applikation zu entwickeln mit Java und das in einer Woche. 

Aber in gesamten gesehen, kam ich gut voran hat zum Glück alles funktioniert. Wo ich noch entäuscht bin ist, dass ich keine Zeit hatte um komplett eine eigene Idee aufzustellen. 





