<img src="https://github.com/wasny0ps/TIMTAL-CTF-Writeups/blob/main/2022/TIMTAL%20IoT/img/index.png">

## Exploration

Looking at robots.txt and there is hex code.

```hex
76 65 72 79 73 65 63 72 65 74
```
Decode it.

<img src="https://github.com/wasny0ps/TIMTAL-CTF-Writeups/blob/main/2022/TIMTAL%20IoT/img/hex.png">

Let's go to /verysecret/ directory. It seems nothing in this page.
<img src="https://github.com/wasny0ps/TIMTAL-CTF-Writeups/blob/main/2022/TIMTAL%20IoT/img/secret.png">

Check the source code. In the ```<p>``` tag, there is a php code.
```php
include "v_connection.php";
$username=$_POST["username"];
$query=$bgl->prepare("SELECT * FROM users WHERE username=:username");
$query->execute(array("username"=>$username));
$row=$query->rowCount();
if ($row > 0) 
{
	$pass=$_POST["password"];
	$password=$_POST["pass"];
  if ($pass !== "240610708") 
  {
	  if ((md5($pass))==(md5($password))) 
	  {
		  echo "1";
	  }
	  else
	  {
		  echo "Wrong password";
	  }
  } 
  else
  {
	  echo "Wrong password";
  }
} 
else 
{
		echo "Wrong username";
}
```
Go to login.php page.
