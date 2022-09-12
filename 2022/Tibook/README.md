<img src="https://github.com/wasny0ps/TIMTAL-CTF-Writeups/blob/main/2022/Tibook/img/main.png">

## Reconnaissance

I went to **robots.txt** and find this.
```php
<?php 

class register {
public $name ="name";
public $username = "username";
public $password = "password";
}
$one = new register();

$a = serialize($one);
$test = unserialize($argv[1]);
$test->username=$_POST['username'];
$check = $test->username - 1337;
if ($check == "ADMIN") 
{
echo "1";
}
else 
{
echo "No flag for you!! Better luck next time!";
}
?>
```

There is class called ```register()``` so I navigated **register.php**.
<img src="https://github.com/wasny0ps/TIMTAL-CTF-Writeups/blob/main/2022/Tibook/img/register.png">
