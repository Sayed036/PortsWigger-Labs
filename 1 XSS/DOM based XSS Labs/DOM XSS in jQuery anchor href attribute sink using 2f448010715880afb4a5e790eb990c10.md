# DOM XSS in jQuery anchor href attribute sink using location.search source

- Given : This lab contains a DOM-based cross-site scripting vulnerability in the submit feedback page. It uses the jQuery library's `$` selector function to find an anchor element, and changes its `href` attribute using data from `location.search`. To solve this lab, make the "back" link alert `document.cookie`.

# SOLUTION -

### Step 1: Submit the feedback and open Inspect

- First, submit the feedback form.
- After submission, **open browser Inspect (Developer Tools)**.
- In the HTML, you can clearly see a JavaScript function using **`.attr()`**.

---

### Step 2: Understand what the code is doing

- The function targets an element with id **`backLink`**.
- This element is an **`<a>` tag (Back button)**.
- When the feedback is submitted, the application:
    - Takes the **returnPath value from the URL**
    - Inserts it into the **`href` attribute** of the Back button
- When the user clicks the Back button, the browser **executes whatever is inside the `href` attribute**.

---

![hj1.png](DOM%20XSS%20in%20jQuery%20anchor%20href%20attribute%20sink%20using/hj1.png)

### Step 3: Identify the vulnerability

- The **returnPath parameter is user-controlled**
- There is **no validation or filtering**
- The value is directly assigned to:
    
    ```jsx
    attr("href", returnPath)
    ```
    
- This creates a **DOM-based XSS vulnerability**

---

### Step 4: Exploit the vulnerability

- We take advantage of the `.attr()` function.
- Instead of a normal path like `/`, we inject a **JavaScript URI**.

### Payload used:

```jsx
javascript:alert(document.cookie)
```

---

### Step 5: Modify the URL

### Original URL:

```
https://0a5600ef037a1d54804a17ff00c2001e.web-security-academy.net/feedback?returnPath=/
```

### Modified URL:

```jsx
https://0a5600ef037a1d54804a17ff00c2001e.web-security-academy.net/feedback?returnPath=javascript:alert(document.cookie)
```

---

![hj2.png](DOM%20XSS%20in%20jQuery%20anchor%20href%20attribute%20sink%20using/hj2.png)

### Step 6: Trigger the XSS

- After modifying the URL, press **Enter**.
- Now click the **Back** button.
- The `href` attribute contains the JavaScript payload.
- When clicked, the browser executes the payload and shows the alert.

---

# Result

- The JavaScript payload is executed successfully.
- **DOM-based XSS is confirmed**
- **Lab solved 🎉**