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
Go to login.php page and research the code.
```html
<form id="login-form" name="login-form" method="post">
					<div class="mb-3">
						<label class="form-label">Username</label>
						<input type="text" id="username" name="username" class="form-control"required>
					</div>
					<div class="mb-3">
						<label class="form-label">Password</label>
						<input type="password" id="password" name="password" class="form-control"required>
					</div>
					<input type="hidden" id="pass" name="pass" value="240610708">
					<button type="submit" class="btn btn-primary">Login</button>
</form>
```
Based on the source code we found in the very secret directory, the ```pass``` variable must be different from "240610708" in order to enter, and the md5 encrypted hash values of the pass and password variables must be the **same**. I set the value of 1 to both the pass and password variables and entered the username as **admin** and logged in.

<img src="https://github.com/wasny0ps/TIMTAL-CTF-Writeups/blob/main/2022/TIMTAL%20IoT/img/wasny.png">

Decode this code with Base64 and get the flag.

<img src="https://github.com/wasny0ps/TIMTAL-CTF-Writeups/blob/main/2022/TIMTAL%20IoT/img/flag.png">
 
> FLAG{getwellsoon+_wasy}

**_by wasny0ps_**
