<img src="https://miro.medium.com/max/630/1*x0pAvH_cWU8VaBmxAe7T7w.png">

## Exploration
In the first step, click the login button and look at the ```source code``` on the login page. Then find the username as **wasny** in the comment code.

```html
<form name="sign-form" id='sign-form' class="form-border" method="post">
   <div class="field-set">
    <input type='text' name='username' id='username' class="form-control" placeholder="username">
  </div>
<div class="field-set">
  <input type='password' name='password' id='password' class="form-control" placeholder="password">
</div>
<!-- Catch Up wasny -->
<div class="field-set">
  <input type='submit' id='login' value='Log In' class="btn btn-main btn-fullwidth color-2">
</div>
 <div class="clearfix"></div>
   <div class="spacer-single"></div>
 </form>
```
When we looking at cokkies, there is cokkie named **guest** as hash and it was encoded with Base64. Decode it in Cyber Chef
<img src="https://miro.medium.com/max/630/1*knilbiqdlBXeOKbRIvlPGg.png">

Result is JSON format.

<img src="https://github.com/wasny0ps/TIMTAL-CTF-Writeups/blob/main/2022/NFT%20Marketplace/img/cyberchef.png">

Listen the network with BurpSuite and log in. Authentication page welcome us.

<img src="https://miro.medium.com/max/382/1*mDORSfR8Zd5hvCMHYVi1Bw.png">

Check network and find **wasny1234@gmail.com** which is wasny's email address.
<img src="https://miro.medium.com/max/630/1*M-O6ba1VgJN6DWwyRUvZdQ.png">
