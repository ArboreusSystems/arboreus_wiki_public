# Install Gitolite, Redmine, Apache on FreeBSD 11.

This installation guide done in the jail operated by Ezjail on Freebsd 11 equipped Nano text editor. The installation process done under the root.

The applications manifest:
* Gitolite: gitolite-3.6.8,1
* Apache: apache-2.4.35
* MySQl: mysql56-server-5.6.41_2
* Redmine: redmine-3.4.6

#### 1. Install Gitolite

On Server:
```console
$ cd /usr/ports/devel/git && make install clean
$ cd /usr/ports/devel/gitolite && make install clean 

>>> NOTICE!
>>> Add the user at time of configuring Gitolite

$ chsh -s /usr/local/bin/bash git
$ chmod g-w /path/to/git/
$ mkdir /path/to/git && chown git:git /path/to/git
$ pw usermod git -d /path/to/git
```
On Client:
```console
>>> NOTICE!
>>> Copy the user SSH key.pub to /tmp on server
```
On Server:
```console
$ su - git
$ gitolite setup -pk /tmp/kirilov.pub
$ cd ~
$ exit
$ nano /path/to/git/.gitolite.rc

>>> NOTICE!
>>> Change the permission for repository folders in the .gitolite.rc

>>> UMASK                           =>  0027,

$ exit
```

#### 2. Install MySQL

```console
$ cd /usr/ports/databases/mysql55-server/ && make BATCH=yes install clean
$ nano /etc/rc.conf

>>> NOTICE!
>>> Add to rc.conf 
>>> # MySQL Daemon
>>> mysql_enable="YES"

$ chsh -s /usr/local/bin/bash mysql
$ mkdir /path/to/mysql/db/folder /path/to/mysql/db/folder/tmp /path/to/mysql/db/folder/secure 
$ pw usermod mysql -d /path/to/mysql/db/folder
$ chown -R mysql:mysql /path/to/mysql/db/folder
$ service mysql-server start
$ mysql_secure_installation

>>> NOTICE!
>>> Do the improving of security 

$ mysql -u root -p

>>> > UPDATE mysql.user set user = 'your_user_name' where user = 'root';
>>> > flush privileges;
>>> > CREATE DATABASE redmine;
>>> > CREATE USER 'redmine'@'localhost' IDENTIFIED BY 'password';
>>> > GRANT ALL ON redmine.* TO 'redmine'@'localhost';
>>> > exit

$ mysql -u your_user_name -p

>>> > exit

$ mysql -u redmine -p

>>> > SHOW DATABASES;
>>> > exit
```

#### 3. Install Apache

```console
$ pkg install apr 

>>> NOTICE!
>>> There was found the problem with installing this package through the ports, available only like package

$ cd /usr/ports/www/apache24/ && make BATCH=yes install clean
$ chsh -s /usr/local/bin/bash www
$ mkdir /path/to/www /path/to/www/log /path/to/www/cgi-bin /path/to/www/default
$ cd /path/to/www/log && touch httpd-error.log && touch httpd-access.log && touch httpd-ssl_request.log
$ pw usermod www -d /path/to/www
$ nano /etc/rc.conf

>>> NOTICE!
>>> Add this line to rc.conf 
>>> # Apache start
>>> apache24_enable="YES"

$ chown -R www:www /path/to/www
```

#### 4. Install Ruby, Ruby-Gems, Ruby-Iconv

```console
$ cd /usr/ports/devel/ruby-gems/ && make install clean
$ gem install iconv -v 1.0.5 

>>> NOTICE!
>>> If need  - change the version

$ cd /usr/ports/graphics/ImageMagick/ && make install clean
$ gem install bundler
$ gem install mysql2
```


#### 5. [Generate SSL](https://github.com/ArboreusSystems/arboreus_wiki_public/blob/master/freebsd/self_signed_ssl_certificate_creating.md)

#### 6. Install Redmine

```console
$ mkdir /path/to/www/redmine
$ cd /path/to/www/redmine
$ curl http://www.redmine.org/releases/redmine-3.4.6.tar.gz --output redmine.tar.gz 

>>> NOTICE!
>>> Download and extract it from archive

$ bundle install --without development test postgresql sqlite
$ gem install passenger
$ passenger-install-apache2-module
$ cp /usr/local/etc/apache24/httpd.conf /usr/local/etc/apache24/httpd.conf.default && nano /usr/local/etc/apache24/httpd.conf
$ cd /usr/local/etc/apache24/Includes && nano passenger.conf

>>> NOTICE!
>>> Add this lines to passenger.conf

>>>LoadModule passenger_module /usr/local/lib/ruby/gems/2.4/gems/passenger-5.3.4/buildout/apache2/mod_passenger.so
>>>   <IfModule mod_passenger.c>
>>>     PassengerRoot /usr/local/lib/ruby/gems/2.4/gems/passenger-5.3.4
>>>     PassengerDefaultRuby /usr/local/bin/ruby24
>>>   </IfModule>

$ cd /usr/local/etc/apache24/Includes && nano virtual_hosts.conf

>>> NOTICE!
>>> Add this lines to virtual_hosts.conf

>>> Listen 60001
>>> SSLCipherSuite HIGH:MEDIUM:!MD5:!RC4
>>> SSLProxyCipherSuite HIGH:MEDIUM:!MD5:!RC4
>>> SSLHonorCipherOrder on
>>> SSLProtocol all -SSLv3
>>> SSLProxyProtocol all -SSLv3
>>> SSLPassPhraseDialog  builtin
>>> SSLSessionCache        "shmcb:/var/run/ssl_scache(512000)"
>>> SSLSessionCacheTimeout  300

>>> PassengerMaxPoolSize 3
>>> PassengerPoolIdleTime 150
>>> PassengerMaxInstancesPerApp 1

>>> <VirtualHost _default_:8080>

>>>    DocumentRoot "/path/to/www/default"
>>>    ServerName server.name:8080
>>>    ServerAdmin mail@server.domain
>>>    ErrorLog "/path/to/www/log/httpd-error.log"
>>>    TransferLog "/path/to/www/log/httpd-access.log"

>>>    SSLEngine on
>>>    SSLCertificateFile "/path/to/www/ssl/keys/server.crt"
>>>    SSLCertificateKeyFile "/path/to/www/ssl/kys/server.key"

>>>    <FilesMatch "\.(cgi|shtml|phtml|php)$">
>>>        SSLOptions +StdEnvVars
>>>    </FilesMatch>

>>>    <Directory "/path/to/www/cgi-bin">
>>>        SSLOptions +StdEnvVars
>>>    </Directory>

>>>    Alias /redmine "/path/to/www/redmine/"

>>>    <Directory /path/to/www/redmine>
>>>        AllowOverride all
>>>        Require all granted
>>>        Options +Indexes +FollowSymLinks -MultiViews
>>>        Order allow,deny
>>>        Allow from all
>>>        RailsEnv production
>>>        PassengerAppRoot /path/to/www/redmine
>>>        PassengerUser www
>>>        PassengerGroup git
>>>        RailsBaseURI /redmine
>>>    </Directory>

>>>    CustomLog "/path/to/www/log/httpd-ssl_request.log" \
>>>          "%t %h %{SSL_PROTOCOL}x %{SSL_CIPHER}x \"%r\" %b"

>>> </VirtualHost>

$ nano /usr/local/etc/apache24/httpd.conf

>>> NOTICE!
>>> Add this lines to httpd.conf

>>>    ServerName server.name:8080
>>>    ServerAdmin mail@server.domain

>>> LoadModule ssl_module libexec/apache24/mod_ssl.so
>>> LoadModule socache_shmcb_module libexec/apache24/mod_socache_shmcb.so

$ cp /path/to/www/redmine/config/database.yml.example /path/to/www/redmine/config/database.yml
$ nano /path/to/www/redmine/config/database.yml

>>> NOTICE!
>>> Install the DB settings to Redmine configuration 

>>> production:
>>>   adapter: mysql2
>>>   database: redmine
>>>   host: localhost
>>>   username: redmine
>>>   password: "password"
>>>   encoding: utf8

$ cp /path/to/www/redmine/config/configuration.yml.example //path/to/www/redmine/config/configuration.yml
$ nano /path/to/www/redmine/config/configuration.yml

>>> email_delivery:
>>>     delivery_method: :smtp
>>>     smtp_settings:
>>>       enable_starttls_auto: true
>>>       address: "smtp.gmail.com"
>>>       port: 587
>>>       domain: "smtp.gmail.com"
>>>       authentication: :plain
>>>       user_name: "your_mail@gmail.com"
>>>       password: “password_here”

$ cd /path/to/www/redmine
$ gem install bundler
$ bundle install --without development test
$ bundle exec rake generate_secret_token
$ RAILS_ENV=production bundle exec rake db:migrate
$ RAILS_ENV=production bundle exec rake redmine:load_default_data
$ chown -R www:www /path/to/www/
$ pw usermod www -G git
$ service apache24 restart
$ bundle exec rails server webrick -e production
```

#### 7. Fix Redmine + Git "no-color" problem

```console
$ nano /usr/local/sbin/git

>>> NOTICE!
>>> Add this lines to this /usr/local/sbin/git

>>> #!/usr/local/bin/bash
>>> 
>>> # The latest git version (2.14.1) removes the --no-color option which breaks existing redmine/git
>>> # support.  We remove this option from the provided arguments until redmine fixes this,
>>> # presumably in redmine 3.4.3
>>> # Issue #305
>>> 
>>> REAL_GIT="/usr/local/bin/git"
>>> $REAL_GIT "${@%--no-color}"

$ chmod +x /usr/local/sbin/git
$ /usr/local/sbin/git —version —no-color
$ nano /path/to/www/redmine/config/configuration.yml

>>> NOTICE!
>>> Add the path to fixed Git into the Redmine configuration file and restart Apache

>>> scm_git_command: /usr/local/sbin/git
```