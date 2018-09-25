# Self-signed SSL certificate creating.

The creating the SSL certificate possible in some ways 

* First way
```console
$ mkdir /path/to/certificte/location && cd /path/to/certificte/location
$ openssl req -x509 -nodes -days 1000 -newkey rsa:2048 -keyout /path/to/certificte/location/selfsigned.key -out /path/to/certificte/location/selfsigned.crt
```
* Second way
```console
$ mkdir /path/to/certificte/location && cd /path/to/certificte/location
$ openssl genrsa -des3 -out server.key 2048
$ openssl rsa -in server.key -out server.key.insecure
$ mv server.key server.key.secure && mv server.key.insecure server.key
$ openssl req -new -key server.key -out server.csr

Country Name (2 letter code) [AU]:AU
State or Province Name (full name) [Some-State]:Some-State
Locality Name (eg, city) []:City
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Company
Organizational Unit Name (eg, section) []:Unit
Common Name (e.g. server FQDN or YOUR name) []:fqdn.server
Email Address []:your@own.mail
Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:

$ openssl x509 -req -days 1000 -in server.csr -signkey server.key -out server.crt
```
