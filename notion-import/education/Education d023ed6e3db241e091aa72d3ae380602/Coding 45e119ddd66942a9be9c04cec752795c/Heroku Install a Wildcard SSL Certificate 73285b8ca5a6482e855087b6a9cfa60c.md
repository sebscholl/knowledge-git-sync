# Heroku Install a Wildcard SSL Certificate

Last Edited: December 19, 2019 11:43 PM

Nginx instructions: [https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content&actpl=CROSSLINK&id=SO17664](https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content&actpl=CROSSLINK&id=SO17664)

GeoTrust Login: [https://products.geotrust.com/orders/orderinformation/authentication.do](https://products.geotrust.com/orders/orderinformation/authentication.do)

Email: [sebastian@rampex.com](mailto:sebastian@rampex.com)

Order ID: 16928245

Pop: [https://mail.hostedemail.com/?_task=mail&_mbox=INBOX](https://mail.hostedemail.com/?_task=mail&_mbox=INBOX)

openssl genrsa -des3 -out server.pass.key 2048

...

Enter pass phrase for server.pass.key:

Verifying - Enter pass phrase for server.pass.key:

openssl rsa -in server.pass.key -out server.key

openssl req -nodes -new -key server.key -out server.csr

...

Country Name (2 letter code) [AU]:US

Common Name (eg, YOUR name) []:[www.example.com](http://www.example.com/)

…

Congratulations! RapidSSL has approved your request for a RapidSSL Wildcard certificate. Your certificate is included at the end of this email.

INSTALLATION INSTRUCTIONS

1. INSTALL CERTIFICATE:

Install the X.509 version of your certificate included at the end of this e-mail.

For installation instructions for your SSL Certificate, go to:

[https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content&id=INFO2699](https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content&id=INFO2699)

2. INTERMEDIATE CERTIFICATE ADVISORY:

You MUST install the RapidSSL intermediate Certificate on your server together with your Certificate or it may not operate correctly.

** MICROSOFT IIS and TOMCAT USERS

Microsoft and Tomcat users are advised to download a PKCS #7 formatted certificate from the GeoTrust User Portal:

[https://products.geotrust.com/orders/orderinformation/authentication.do](https://products.geotrust.com/orders/orderinformation/authentication.do). PKCS #7 is the default format used by these vendors during installation and includes the intermediate CA certificate.

You can get your RapidSSL Intermediate Certificates at:

[https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content&id=INFO1548](https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content&id=INFO1548)

3. CHECK INSTALLATION:

Ensure you have installed your certificate correctly at:

[https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content&id=SO9556](https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content&id=SO9556)

4. INSTALL THE RAPIDSSL SITE SEAL:

Additionally, as part of your SSL Certificate Service, you are entitled to display the RapidSSL Site Seal - recognized across the Internet and around the world as a symbol of authenticity, security, and trust - to build consumer confidence in your Web site.

Installation instructions for the RapidSSL Site Seal can be found on the following link:

[https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content&id=SO14424&actp=LIST&viewlocale=en_US](https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content&id=SO14424&actp=LIST&viewlocale=en_US)

[https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content&actp=CROSSLINK&id=SO16222](https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content&actp=CROSSLINK&id=SO16222)

If you require additional technical support please contact your Reseller.

Certificates

[https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content&id=INFO1548](https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content&id=INFO1548)

[Untitled](Heroku%20Install%20a%20Wildcard%20SSL%20Certificate%2073285b8ca5a6482e855087b6a9cfa60c/Untitled%20Database%20e8140b06d8b649558ff05210a6501cb8.csv)