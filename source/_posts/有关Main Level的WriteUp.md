# WriteUp
[TOC]
##Main Level 1
这道题是入门题，非常简单，也有视频教程。教会我们查看网页的源代码
可以在网页**右键**，然后查看，或者**Ctrl+U**也可以查看。
第一题的源代码我们可以看到又如下字段
```
<!-- <script src="https://cdn.socket.io/socket.io-1.2.1.js"></script> -->
        <!-- username: in, password: out -->
```
由此得到第一题答案
##Main Level 2
第二题也是同样查看源代码
```
   <label for="user">Username:</label> <span style="color: #000000">resu</span>
   <input type="Text" name="user" id="user" autocomplete="off"><br>
   <label for="user">Password:</label> <span style="color: #000000">ssap</span>
   <input type="Password" name="pass" id="pass" autocomplete="off"><br>
   <input type="submit" value="Submit" class="button">
```
可以看到**color**这里是**#000000**也就是全黑，所以猜测是不是有东西隐藏在背景中，其实这个属性后的东西也就是**resu**和**ssap**就是隐藏的，第二题得解
##Main Level 3
这道题用到了**JavaScript**，什么是**JavaScript**，这里有介绍
>JavaScript一种直译式脚本语言，是一种动态类型、弱类型、基于原型的语言，内置支持类型。它的解释器被称为JavaScript引擎，为浏览器的一部分，广泛用于客户端的脚本语言，最早是在HTML（标准通用标记语言下的一个应用）网页上使用，用来给HTML网页增加动态功能。--[百度百科](https://baike.baidu.com/item/javascript/321142?fr=aladdin)

查看源代码，搜索关键字
```
<script type='text/javascript'> $(function(){ $('.level-form').submit(function(e){ if(document.getElementById('user').value == 'heaven' && document.getElementById('pass').value == 'hell') { } 
else { e.preventDefault(); alert('Incorrect login') } })})</script>
```
这段的意思是如果**user**的**value**为**heaven**，密码为**hell**时正常运行，否则就显示**Incorrect login**
这也就知道了用户名和密码了
其实Level 1-3官方都有出视频带着你一步步的怎么入门这个东西，算是对新手很友好的一个榜了，每道题都有供讨论的地方，有些题还有hint，这题开始就需要自己来探索了
##Main Level 4
这题老样子看源代码
```
<input type="hidden" name="passwordfile" value="../../extras/ssap.xml">
```
猜测密码藏在了这个目录下的这个文件里，前缀已经省略，实验了几次[这个网址](https://www.hackthis.co.uk/levels/extras/ssap.xml)可以访问到目录，继续查看源代码
```
<name>Admin</name>
<username>999</username>
<password>911</password>
```
得到此题的答案
##Main Level 5
这道题跟之前的不同，一上来就弹出了一个框要求我输入密码，忽略不管，**hint**提示是**JavaScript**，查看源代码，以**JavaScript**为关键字
```
<script language="JavaScript" type="text/javascript">
            var pass;
            pass=prompt("Password","");
            if (pass=="9286jas") {
                window.location.href="/levels/main/5?pass=9286jas";
```
这已经很明显了，**pass**是什么。
##Main Level 6
这道题一上来给了一个下拉框，先看一下**hint**
>This page is coded to only let in one user (Ronald). But there is no Ronald?! You will need to find a way to add him to the list.

大意是这个只有在提交**Ronald**的时候才能通过，但下拉列表里没有这个，所以我们得自己构造，这里就要用道开发者工具，也就是编辑源代码的，大部分浏览器可以使用**F12**达到这一功能，![Alt text](./images/1544714883960.png)
大致就是在这里修改一个，然后就可以提交了
##Main Level 7
这道题看一下**hint**
>The password is again stored in a txt file. This time however it is not as straight forward as viewing the source.
>You wouldn't even find the page by using a search engine as search bots have been excluded.

密码藏在了一个文本里，这个文本无法被搜索引擎找到，这已经说的很明显了，储存哪些目录不能被网络爬虫所找到的这个文本**robots.txt**,以下是关于这个的介绍
>robots是网站跟爬虫间的协议，用简单直接的txt格式文本方式告诉对应的爬虫被允许的权限，也就是说robots.txt是搜索引擎中访问网站的时候要查看的第一个文件。当一个搜索蜘蛛访问一个站点时，它会首先检查该站点根目录下是否存在robots.txt，如果存在，搜索机器人就会按照该文件中的内容来确定访问的范围；如果该文件不存在，所有的搜索蜘蛛将能够访问网站上所有没有被口令保护的页面。--[百度百科](https://baike.baidu.com/item/robots/5243374?fr=aladdin)

看到这些东西
```
User-agent: *
Allow: /
Disallow: /contact.php
Disallow: /inbox/
Disallow: /levels/
Disallow: /levels/extras/userpass.txt
Disallow: /users/
Disallow: /ctf/8/php/*
```
密码藏在哪里，直接访问就能得到了
##Main Level 8
这道题先看**hint**
这道题跟**Level 4**方法差不多，但是最后需要**2进制**自行转换成**16进制**
```
<input type="hidden" name="passwordfile" value="extras/secret.txt">
```
##Main Level 9
这道题有点意思，当时让我想了有一段时间，**hint**意思是开发者开发了一个功能，使你可以找回密码，也就是邮件忘记密码功能的应用，所以点那个**Request details**，然后源代码，看看有什么名堂
```
<label for="email1">Email:</label>
  <input type="text" name="email1" id="email1" autocomplete="off"><br>
  <input type="hidden" name="email2" id="email2" value="admin@hackthis.co.uk" autocomplete="off">
  <input type="submit" value="Submit" class="button">
```
 这里我们得到了一个邮箱*admin@hackthis.co.uk*，试着讲这个输入，但是失败了。
 ![Alt text](./images/1544718369046.png)
就这里当时困扰了我好久，不是这个邮箱那是哪个邮箱啊，后面上该题的讨论区域，摸索到了一点门道。
既然不让信件发送到官方的邮箱，那我可以把这个发送到自己邮箱啊，就把**后面的这个验证值改成了自己邮箱**，然后输入自己邮箱，成功解决。
##Main Level 10
基础题的最后一题
说这道题啊用了加密手段，不管怎么说先进源代码
```
 <input type="hidden" name="passwordfile" value="level10pass.txt">
```
 密码藏在这个文件里，根据前几题，也能知道目录在哪里，打开文本是这个
 >69bfe1e6e44821df7f8a0927bd7e61ef208fdb25deaa4353450bc3fb904abd52:f1abe1b083d12d181ae136cfc75b8d18a8ecb43ac4e9d1a36d6a9c75b6016b61
 
 这个是**MD5**，找个网站解密就行，至此**Main**关卡所有题结束