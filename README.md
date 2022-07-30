# Public-Key-Infrastructure
# Task 1
Copy the configuration file into current directory:
```
cp /usr/lib/ssl/openssl.cnf ./openssl.cnf 
 ```
create new sub-directories and files according to what it specifies in its  ```[ CA_default ]```section:
```
dir = ./demoCA # Where everything is kept
certs = $dir/certs # Where the issued certs are kept
crl_dir = $dir/crl # Where the issued crl are kept
new_certs_dir = $dir/newcerts # default place for new certs.
database = $dir/index.txt # database index file.
serial = $dir/serial # The current serial number
```
Simply create an empty file for ```index.txt```, put a single number in string format in serial:
```
mkdir PKI
cp "/usr/lib/ssl/openssl.cnf" "/home/seed/PKI/"
mkdir demoWK
cd demoWK
mkdir certs crl newcerts
echo 1000 > serial
gedit index.txt
```

![task1](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/1.PNG)

Start to generate the self-signed certificate for the CA:

return to the parent directory
```
cd ..
openssl req -new -x509 -keyout ca.key -out ca.crt -config openssl.cnf 
```
When asked to type PEM pass phrase, remember the password you typed (e.g. I use ```seeddes```). It will then ask you to fill in some information, you can skip it by Enter, except for those required by policy_match.
```
Generating a 2048 bit RSA private key
...................+++
.............................................................................+++
writing new private key to 'ca.key'
Enter PEM pass phrase:
Verifying - Enter PEM pass phrase:
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:PK
State or Province Name (full name) [Some-State]:Panjab
Locality Name (eg, city) []:swl
Organization Name (eg, company) [Internet Widgits Pty Ltd]:UOS
Organizational Unit Name (eg, section) []:UOSahiwal
Common Name (e.g. server FQDN or YOUR name) []:Annie
Email Address []:test@test.com
```


![task1](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/2.PNG)

# Task 2
As a root CA, we are ready to sign a digital certificate for SEEDPKILab2020.com.

# Step 1: Generate public/private key pair
Generate an RSA key pair. Provide a pass phrase (e.g. I use ```seeddes```) to encrypt the private key in ```server.key``` using ```AES-128 encryption ```algorithm.
```
openssl genrsa -aes128 -out server.key 1024
```
To see the actual content in ```server.key``` (pass phrase required):
```
openssl rsa -in server.key -text
```
Our Private Key is
```

Private-Key: (1024 bit)
modulus:
    00:b9:a6:ae:c1:a1:db:0d:40:5b:1e:33:c7:85:d8:
    10:39:e2:ba:54:dd:0a:43:58:72:af:2c:12:ae:ba:
    9e:1a:47:f0:b9:62:70:3e:e7:0d:8d:32:57:a6:e5:
    8a:8d:8b:99:88:9f:5e:5d:2d:c2:95:b8:c1:d3:6e:
    f1:ba:69:9c:26:0e:be:0c:d6:48:db:b7:45:6b:ac:
    ef:43:f7:76:c8:46:0c:14:d8:fe:aa:39:ad:eb:c3:
    d4:73:51:b6:80:3f:50:60:a5:64:0a:c3:0f:ea:46:
    6e:5d:e9:1d:0a:f5:db:86:0f:bc:3e:19:15:ea:2b:
    1d:fd:b3:4a:1d:e7:9c:97:61
publicExponent: 65537 (0x10001)
privateExponent:
    6e:d5:ba:43:53:b4:09:47:40:9e:d9:5e:e6:e3:45:
    5c:a9:a5:80:80:ae:5d:e2:72:25:6e:74:80:e8:5c:
    f7:67:b7:a9:95:c1:59:6c:6b:c4:be:27:62:36:6b:
    ef:71:46:6a:30:6b:0f:c9:ff:ff:8e:db:f8:b4:a5:
    90:1a:f8:e3:21:62:0e:59:0b:12:5e:45:d8:99:ff:
    4a:11:2b:5c:b7:e5:e7:13:85:d8:2e:8d:fb:dd:f9:
    57:fd:b1:3f:5a:6b:cc:44:42:f2:cc:9e:e0:bb:54:
    51:b2:20:68:4b:87:c0:76:02:a6:6b:0d:9a:be:5b:
    28:ec:66:71:bf:89:09:d9
prime1:
    00:f6:af:cc:88:a5:79:bc:d2:f4:8c:29:50:18:ca:
    9d:65:2f:12:8e:76:e1:0e:ab:d3:8b:40:a0:73:cb:
    08:09:ee:bd:66:5c:1a:ca:9b:8f:f1:04:42:04:64:
    5d:7a:05:00:12:c2:02:42:6f:64:47:d8:ce:fe:1e:
    7b:e8:fa:4c:ef
prime2:
    00:c0:a8:fb:1f:b5:dd:29:12:25:ae:a6:ce:c4:a9:
    54:1d:f1:c1:c1:4e:2b:9f:b8:71:ba:a1:6b:92:a7:
    8f:52:08:34:36:34:00:fc:2c:4a:fb:85:37:5e:f8:
    2e:50:aa:cd:a9:4f:d6:cd:d1:3c:9e:b3:5b:8a:ff:
    a6:67:9e:00:af
exponent1:
    5e:8b:d6:5a:71:01:8d:8b:54:ca:fb:72:85:6d:f2:
    91:3b:4f:63:66:d0:af:2c:cf:f1:49:1d:b6:03:94:
    db:29:b3:51:ad:ef:5e:c3:ec:91:35:4e:90:1c:5f:
    6f:4a:c7:52:69:25:30:8d:3c:e4:04:86:a1:02:d1:
    fe:e3:1f:e5
exponent2:
    7a:26:a9:91:e1:6c:e7:ad:69:d6:e2:4c:16:c4:85:
    60:b6:f7:71:e8:6e:20:46:81:55:23:23:61:48:7b:
    c6:37:0d:63:90:75:4f:6d:85:dd:13:09:98:5d:22:
    80:62:cb:22:9e:4c:43:12:76:ac:e8:6b:12:26:25:
    0b:6d:52:61
coefficient:
    77:82:59:c8:6f:71:6c:3f:51:30:41:e9:70:f1:a6:
    3b:7d:ae:ae:5a:c3:e6:bf:fe:bc:43:9d:f0:2d:9d:
    63:fc:a4:45:be:da:4c:22:3d:b7:b3:1e:03:46:0b:
    cf:a2:ae:89:02:4b:99:af:9b:97:1d:89:6e:be:d6:
    15:90:a4:8c
writing RSA key
-----BEGIN RSA PRIVATE KEY-----
MIICWwIBAAKBgQC5pq7BodsNQFseM8eF2BA54rpU3QpDWHKvLBKuup4aR/C5YnA+
5w2NMlem5YqNi5mIn15dLcKVuMHTbvG6aZwmDr4M1kjbt0VrrO9D93bIRgwU2P6q
Oa3rw9RzUbaAP1BgpWQKww/qRm5d6R0K9duGD7w+GRXqKx39s0od55yXYQIDAQAB
AoGAbtW6Q1O0CUdAntle5uNFXKmlgICuXeJyJW50gOhc92e3qZXBWWxrxL4nYjZr
73FGajBrD8n//47b+LSlkBr44yFiDlkLEl5F2Jn/ShErXLfl5xOF2C6N+935V/2x
P1przERC8sye4LtUUbIgaEuHwHYCpmsNmr5bKOxmcb+JCdkCQQD2r8yIpXm80vSM
KVAYyp1lLxKOduEOq9OLQKBzywgJ7r1mXBrKm4/xBEIEZF16BQASwgJCb2RH2M7+
Hnvo+kzvAkEAwKj7H7XdKRIlrqbOxKlUHfHBwU4rn7hxuqFrkqePUgg0NjQA/CxK
+4U3XvguUKrNqU/WzdE8nrNbiv+mZ54ArwJAXovWWnEBjYtUyvtyhW3ykTtPY2bQ
ryzP8UkdtgOU2ymzUa3vXsPskTVOkBxfb0rHUmklMI085ASGoQLR/uMf5QJAeiap
keFs561p1uJMFsSFYLb3cehuIEaBVSMjYUh7xjcNY5B1T22F3RMJmF0igGLLIp5M
QxJ2rOhrEiYlC21SYQJAd4JZyG9xbD9RMEHpcPGmO32urlrD5r/+vEOd8C2dY/yk
Rb7aTCI9t7MeA0YLz6KuiQJLma+blx2Jbr7WFZCkjA==
-----END RSA PRIVATE KEY-----
```



![task1](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/3.PNG)


# Step 2: Generate a Certificate Signing Request (CSR)

Use ```SEEDPKILab2020.com``` as the common name of the certificate request

```
openssl req -new -key server.key -out server.csr -config openssl.cnf
```
Skip the unnecessary information as well, keep the necessary information (required by policy_match consistent with the CA.crt created in Task 1).

![task1](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/4.PNG)

Now, the new Certificate Signing Request is saved in ```server.csr```, which basically includes the company's public key.

The CSR will be sent to the CA, who will generate a certificate for the key (usually after ensuring that identity information in the CSR matches with the server's true identity)
# Step 3: Generating Certificates
In this lab, we will use our own trusted CA to generate certificates.

Use ```ca.crt``` and ```ca.key``` to convert server.csr to ```server.crt```:
```
openssl ca -in server.csr -out server.crt -cert ca.crt -keyfile ca.key \
-config openssl.cnf
```
Our Certificate Is Generated

Using configuration from ```openssl.cnf```
```
Enter pass phrase for ca.key:
Check that the request matches the signature
Signature ok
Certificate Details:
        Serial Number: 4096 (0x1000)
        Validity
            Not Before: Dec 24 12:21:24 2021 GMT
            Not After : Dec 24 12:21:24 2022 GMT
        Subject:
            countryName               = PK
            stateOrProvinceName       = Panjab
            organizationName          = UOS
            organizationalUnitName    = UOSahiwal
            commonName                = SEEDPKILab2020.com
            emailAddress              = test@test.com
        X509v3 extensions:
            X509v3 Basic Constraints: 
                CA:FALSE
            Netscape Comment: 
                OpenSSL Generated Certificate
            X509v3 Subject Key Identifier: 
                AD:9A:79:05:6B:6C:6F:80:6E:1C:63:AA:9B:D9:9D:3E:7D:76:9B:00
            X509v3 Authority Key Identifier: 
                keyid:5B:83:26:FF:14:3F:D5:A8:C6:0C:55:D9:6D:02:81:3E:95:D8:C4:C5

Certificate is to be certified until Dec 24 12:21:24 2022 GMT (365 days)
Sign the certificate? [y/n]:y


1 out of 1 certificate requests certified, commit? [y/n]y
Write out database with 1 new entries
Data Base Updated
```


![task1](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/5.PNG)


# Task 3
# Step 1: Configuring DNS
Open and edit ```/etc/hosts```:
```
sudo vi /etc/hosts
```
Add one line:
```
127.0.0.1 SEEDPKILab2020.com
```
![task3](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/13.PNG)

# Step 2: Configuring the web server
Combine the secret key and certificate into one single file ```server.pem```:
```
cp server.key server.pem
cat server.crt >> server.pem
```
Launch the web server using ```server.pem```:
```
openssl s_server -cert server.pem -www
```

Now, the server is listening on port ```4433```. Browser ```https://seedpkilab2020.com:4433/  ```

![task3a](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/6.PNGG)

# Step 3: Getting the browser to accept our CA certificate.
Search for certificate in Firefox's Preferences page, click on View Certificates and enter certificate manager, click on Authorities tab and import CA.crt. Check Trust this CA to identify web sites.

![task3c](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/7.PNG)

Reload https://seedpkilab2020.com:4433/.

![task3d](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/8.PNG)

# Step 4. Testing our HTTPS website
# Modify one byte in server.pem

![task3e](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/9.PNG)


It's up to which byte you modify. Most bytes make no differences after corrupted. But some will make the certificate invalid.

# Use localhost
When browsing ```https://localhost:4433```, it is reported unsafe HTTPS

![task3g](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/10.PNG)

Because the locolhost has no certificate, the website is using a certificate identified for ```seedpkilab2020.com```.

# Task 4: Deploying Certificate in an Apache-Based HTTPS Website

First make directory in ```/var/www``` and copy ```index.html``` in it.

```
cd /var/www
sudo mkdir SeedDev
sudo cp "/var/www/html/index.html" "/var/www/SeedDev/"
```

![task4a](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/11.PNG)

Now make directory ssl in ```/etc/apache2``` & copy ```crt.pem``` ``` key.pem``` in it
```
cd /etc/apache2/
sudo mkdir ssl
cp server.crt crt.pem
cp server.key key.pem
sudo mv "/home/seed/PKI/crt.pem" "/etc/apache2/ssl"
sudo mv "/home/seed/PKI/key.pem" "/etc/apache2/ssl"
```
![task4b](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/12.PNG)

Open configuration file of Apache HTTPS server:
```
sudo vi /etc/apache2/sites-available/000-default.conf
```
Add the entry and save:
```
<VirtualHost *:80>
ServerName seedpkilab2020.com
DocumentRoot /var/www/SeedDev
DirectoryIndex index.html
</VirtualHost>
```

![task4d](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/14.PNG)

Open configuration file of Apache HTTPS SSL server:
```
sudo vi /etc/apache2/sites-available/default-ssl.conf
```
Add the entry and save:
```
<VirtualHost *:443>
ServerName seedpkilab2020.com
DocumentRoot /var/www/seedpki
DirectoryIndex index.html
SSLEngine On
SSLCertificateFile /etc/apache2/ssl/cert.pem
SSLCertificateKeyFile /etc/apache2/ssl/key.pem
</VirtualHost>
```

![task4e](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/16.PNG)

Test the Apache configuration file for errors
```
sudo apachectl configtest

Enable the SSL module

sudo a2enmod ssl

Restart Apache

sudo service apache2 restart
```

![task4f](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/15.PNG)

As result

![task4g](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/17.PNG)

# Task 5
Generate a certificate for ```instagram.com```
use a password (e.g. I use ```seeddes```):
```
openssl genrsa -aes128 -out instagram.key 1024
```
Use instagram.com as the common name of the certificate request:
```
openssl req -new -key instagram.key -out example.csr -config openssl.cnf
openssl ca -in example.csr -out instafram.crt -cert ca.crt -keyfile ca.key \
-config openssl.cnf
cp instagram.key instagram.pem
cat instagram.crt >> instagram.pem
```
Copy the certificate and private key to the website root folder:
```
sudo mkdir /var/www/instagram
sudo cp instagram.crt instagram.pem /var/www/instagram
```
Config and start the server
On the server VM, open /etc/apache2/sites-available/default-ssl.conf and add the following entry:
```
<VirtualHost *:443>
        ServerName instagram.com
        DocumentRoot /var/www/instagram
        DirectoryIndex index.html

        SSLEngine On
        SSLCertificateFile /var/www/instagram/instagram.crt
        SSLCertificateKeyFile /var/www/instagram/instagram.pem
</VirtualHost>

```
![task5a](https://github.com/abdul9255/Public-Key-Infrastructure/blob/main/5.PNG)

Restart Apache:
```
sudo apachectl configtest
sudo service apache2 restart
```
Config on Victim VM
On the victim VM, modify``` /etc/hosts``` by:
```
sudo vi /etc/hosts
```
add one line before the ending, which emulates a DNS cache positing attack:
```
127.0.0.1	instagram.com
```
To get the ```ca.crt```, listen on a local port like:
```
nc -lvp 4444 > ca.crt
```
Then on the server VM, we send ```ca.crt``` by:
```
cat ca.crt | nc 127.0.0.1 4444
```
Once we receive the file on the victim VM, we install it on Firefox as above.

Now, when browsing https://instagram.com/, the user on this VM actually visit the fake website launched by the malicious server:

# Task 6
Based on Task 5, we can assume if the attacker stole ca.key, which indicates that he/she can easily generate the CA certificate ca.crt by the compromised key:
```
openssl req -new -x509 -keyout ca.key -out ca.crt -config openssl.cnf
```
Then, ca.crt can be used to sign any server's certificate, including the forged ones. The process of such attacks can be described as what we did before, except that we don't even need to deploy the ca.crt on the victim machine because it has already installed the same ca.crt

