# DOM XSS in document.write sink using source location.search

- **Given**  :  This lab contains a DOM-based cross-site scripting vulnerability in the search query     tracking functionality. It uses the JavaScript *document.write* function, which writes data out to the page. The document.write function is called with data from *location.search*, which you can control using the website URL.  To solve this lab, perform a cross-site scripting attack that calls the *alert* function.
- **HINT** : Note, however, that in some situations the content that is written to `*document.write*` includes some surrounding context that you need to take account of in your exploit. For example, you might need to close some existing elements before using your JavaScript payload.
    
    

Solution : 

- 1st entering the normal alert code, checking working or not ?

![image.png](DOM%20XSS%20in%20document%20write%20sink%20using%20source%20locati/image.png)

- nothing happend, but wait we can see our alert code in img tag. which(img tag) also already in <script> tag,  our alert function comment out the  img closing tag. 😂
- now what we can do ?? append the “> for closing the img tag, after that we can insert our *<script> for alert.*
- when we enter our script using “>
- we can see clearly, script runs successfully …hureyyy. also we got the alert messege as well as in the img tag, we can see img tag is closed, after that our script attatched or run successfully.

![image.png](DOM%20XSS%20in%20document%20write%20sink%20using%20source%20locati/image%201.png)

![image.png](DOM%20XSS%20in%20document%20write%20sink%20using%20source%20locati/image%202.png)

Lab Solved 🙂

- but wait, you can use Lab script →   “>document.write(<script>alert(location.search)</script>)
- i used alert(1) script for this lab.