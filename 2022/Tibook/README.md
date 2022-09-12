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

<img src="https://github.com/wasny0ps/TIMTAL-CTF-Writeups/blob/main/2022/Tibook/img/register.png" height="500">

When we look at the source codes of the page on the register page, we can say that these codes we found belong to the **user.php** page.

```js
<script type="text/javascript">

      $(document).ready(function (e) {
        $('#register-form').on('submit',(function(e) {
            e.preventDefault();
            $.ajax({ 
             type: "POST",
             url: "user.php",
             data: $("#register-form").serialize(),
             success: function(data)
             {
                if (data==1) 
                {
                                        window.open("https://siberguvenliklisesi.com/tibook/profile.php","_self");

                }
                else
                {
                    alert(data);
                }
                
             }
         });
        }));
    });
</script>
```
Based on this inference, we must find vulnerability from this code for bypass register part.

## Exploitation
After long researches, I found a vulnerability which we can exploit it. There is **_PHP Object Injection_** vulnerability.
> PHP Object Injection is an application level vulnerability that could allow an attacker to perform different kinds of malicious attacks, such as Code Injection, SQL Injection, Path Traversal and Application Denial of Service, depending on the context. The vulnerability occurs when user-supplied input is not properly sanitized before being passed to the unserialize() PHP function. Since PHP allows object serialization, attackers could pass ad-hoc serialized strings to a vulnerable unserialize() call, resulting in an arbitrary PHP object(s) injection into the application scope.

If we go back to our target code, the following condition should be fulfilled in order to continue: **$username** variable resulting from subtracting 1337 from “username” variable is equal to “ADMIN” text string because of in PHP, the result of comparing a text string with a 0 integer value is TRUE, therefore the condition shall be fulfilled if “username” is not a string anymore and becomes a integer of 1337 (1337 – 1337 = 0) value.

<img src="https://github.com/wasny0ps/TIMTAL-CTF-Writeups/blob/main/2022/Tibook/img/login.png" height="500">

And we are in.
<img src="https://github.com/wasny0ps/TIMTAL-CTF-Writeups/blob/main/2022/Tibook/img/profile.png" height="500">
