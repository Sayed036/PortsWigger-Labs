# 2. Bypass rate limit via Race Condition.

Goal : we need to retrieve password of carlos via bruteforce and  login as a carlos and gain the admin panel, and delete the carlos user.

Steps : 

- intercept the request of login page(user : carlos, password : anything).
- then, send that into intruder. and add($anything$) password to bruteforce.
    - Now password list already given in the Lab section. just copy and paste all password in the list. and make 30 request at a one time.
    - Now do sniper attack, u can see a 302 response. that is the correct password.
    - just copy the url and open in browser. and go to admin panel, delete the carlos user.